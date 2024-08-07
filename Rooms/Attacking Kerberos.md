## Introduction
﻿﻿﻿This room will cover all of the basics of attacking Kerberos the windows ticket-granting service; we'll cover the following:  
- Initial enumeration using tools like Kerbrute and Rubeus
- Kerberoasting
- AS-REP Roasting with Rubeus and Impacket
- Golden/Silver Ticket Attacks
- Pass the Ticket
- Skeleton key attacks using mimikatz
This room will be related to very real-world applications and will most likely not help with any CTFs however it will give you great starting knowledge of how to escalate your privileges to a domain admin by attacking Kerberos and allow you to take over and control a network.  
It is recommended to have knowledge of general post-exploitation, active directory basics, and windows command line to be successful with this room.

### What is Kerberos? -  
Kerberos is the default authentication service for Microsoft Windows domains. It is intended to be more "secure" than NTLM by using third party ticket authorization as well as stronger encryption. Even though NTLM has a lot more attack vectors to choose from Kerberos still has a handful of underlying vulnerabilities just like NTLM that we can use to our advantage.

### Common Terminology -  
- Ticket Granting Ticket (TGT) - A ticket-granting ticket is an authentication ticket used to request service tickets from the TGS for specific resources from the domain.
- Key Distribution Center (KDC) - The Key Distribution Center is a service for issuing TGTs and service tickets that consist of the Authentication Service and the Ticket Granting Service.
- Authentication Service (AS) - The Authentication Service issues TGTs to be used by the TGS in the domain to request access to other machines and service tickets.
- Ticket Granting Service (TGS) - The Ticket Granting Service takes the TGT and returns a ticket to a machine on the domain.
- Service Principal Name (SPN) - A Service Principal Name is an identifier given to a service instance to associate a service instance with a domain service account. Windows requires that services have a domain service account which is why a service needs an SPN set.
- KDC Long Term Secret Key (KDC LT Key) - The KDC key is based on the KRBTGT service account. It is used to encrypt the TGT and sign the PAC.
- Client Long Term Secret Key (Client LT Key) - The client key is based on the computer or service account. It is used to check the encrypted timestamp and encrypt the session key.
- Service Long Term Secret Key (Service LT Key) - The service key is based on the service account. It is used to encrypt the service portion of the service ticket and sign the PAC.
- Session Key - Issued by the KDC when a TGT is issued. The user will provide the session key to the KDC along with the TGT when requesting a service ticket.
- Privilege Attribute Certificate (PAC) - The PAC holds all of the user's relevant information, it is sent along with the TGT to the KDC to be signed by the Target LT Key and the KDC LT Key in order to validate the user.

### AS-REQ w/ Pre-Authentication In Detail - 
The AS-REQ step in Kerberos authentication starts when a user requests a TGT from the KDC. In order to validate the user and create a TGT for the user, the KDC must follow these exact steps. The first step is for the user to encrypt a timestamp NT hash and send it to the AS. The KDC attempts to decrypt the timestamp using the NT hash from the user, if successful the KDC will issue a TGT as well as a session key for the user.
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_1.png" width="50%" height="50%">

### Service Ticket Contents - 
To understand how Kerberos authentication works you first need to understand what these tickets contain and how they're validated. A service ticket contains two portions: the service provided portion and the user-provided portion. I'll break it down into what each portion contains.
- Service Portion: User Details, Session Key, Encrypts the ticket with the service account NTLM hash.
- User Portion: Validity Timestamp, Session Key, Encrypts with the TGT session key.
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_2.png" width="50%" height="50%">

### Kerberos Authentication Overview -
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_3.png" width="50%" height="50%">  
AS-REQ - 1.) The client requests an Authentication Ticket or Ticket Granting Ticket (TGT).  
AS-REP - 2.) The Key Distribution Center verifies the client and sends back an encrypted TGT.  
TGS-REQ - 3.) The client sends the encrypted TGT to the Ticket Granting Server (TGS) with the Service Principal Name (SPN) of the service the client wants to access.  
TGS-REP - 4.) The Key Distribution Center (KDC) verifies the TGT of the user and that the user has access to the service, then sends a valid session key for the service to the client.  
AP-REQ - 5.) The client requests the service and sends the valid session key to prove the user has access.  
AP-REP - 6.) The service grants access

### Kerberos Tickets Overview - 
The main ticket you will receive is a ticket-granting ticket (TGT). These can come in various forms, such as a .kirbi for Rubeus and .ccache for Impacket. A ticket is typically base64 encoded and can be used for multiple attacks.  
The ticket-granting ticket is only used to get service tickets from the KDC. When requesting a TGT from the KDC, the user will authenticate with their credentials to the KDC and request a ticket. The server will validate the credentials, create a TGT and encrypt it using the krbtgt key. The encrypted TGT and a session key will be sent to the user.  
When the user needs to request a service ticket, they will send the TGT and the session key to the KDC, along with the service principal name (SPN) of the service they wish to access. The KDC will validate the TGT and session key. If they are correct, the KDC will grant the user a service ticket, which can be used to authenticate to the corresponding service.

### Attack Privilege Requirements -
- Kerbrute Enumeration - No domain access required 
- Pass the Ticket - Access as a user to the domain required
- Kerberoasting - Access as any user required
- AS-REP Roasting - Access as any user required
- Golden Ticket - Full domain compromise (domain admin) required 
- Silver Ticket - Service hash required 
- Skeleton Key - Full domain compromise (domain admin) required


## Enumeration w/ Kerbrute
﻿Kerbrute is a popular enumeration tool used to brute-force and enumerate valid active-directory users by abusing the Kerberos pre-authentication.  
For more information on enumeration using Kerbrute check out the Attacktive Directory room by Sq00ky - https://tryhackme.com/room/attacktivedirectory  
You need to add the DNS domain name along with the machine IP to /etc/hosts inside of your attacker machine or these attacks will not work for you - `MACHINE_IP  CONTROLLER.local`

### Abusing Pre-Authentication Overview -
By brute-forcing Kerberos pre-authentication, you do not trigger the account failed to log on event which can throw up red flags to blue teams. When brute-forcing through Kerberos you can brute-force by only sending a single UDP frame to the KDC allowing you to enumerate the users on the domain from a wordlist.

### Kerbrute Installation - 
1.) Download a precompiled binary for your OS - https://github.com/ropnop/kerbrute/releases  
2.) Rename kerbrute_linux_amd64 to kerbrute  
3.) `chmod +x kerbrute` - make kerbrute executable

### Enumerating Users w/ Kerbrute -
Enumerating users allows you to know which user accounts are on the target domain and which accounts could potentially be used to access the network.  
1.) cd into the directory that you put Kerbrute  
2.) Download the wordlist to enumerate with [here](https://github.com/Cryilllic/Active-Directory-Wordlists/blob/master/User.txt)  
3.) `./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt` - This will brute force user accounts from a domain controller using a supplied wordlist

----------------------------------------Answer the questions below--------------------------------------------------  
How many total users do we enumerate?  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_4.png" width="50%" height="50%">  
「`./kerburute userenum -d ドメイン名 --dc ドメコンIP Wordlist名 -o 出力ファイル`」で列挙をすると、10個のユーザを確認！  
（名前解決のための`/etc/hosts`ファイルを編集していない場合、`--dc`オプションはIPアドレスが必須になる。）


## Harvesting & Brute-Forcing Tickets w/ Rubeus
Rubeus is a powerful tool for attacking Kerberos. Rubeus is an adaptation of the kekeo tool and developed by HarmJ0y the very well known active directory guru.  
Rubeus has a wide variety of attacks and features that allow it to be a very versatile tool for attacking Kerberos. Just some of the many tools and attacks include overpass the hash, ticket requests and renewals, ticket management, ticket extraction, harvesting, pass the ticket, AS-REP Roasting, and Kerberoasting.  
The tool has way too many attacks and features for me to cover all of them so I'll be covering only the ones I think are most crucial to understand how to attack Kerberos however I encourage you to research and learn more about Rubeus and its whole host of attacks and features here - https://github.com/GhostPack/Rubeus  
Rubeus is already compiled and on the target machine.

### Harvesting Tickets w/ Rubeus - 
Harvesting gathers tickets that are being transferred to the KDC and saves them for use in other attacks such as the pass the ticket attack.  
1.) cd Downloads - navigate to the directory Rubeus is in  
2.) `Rubeus.exe harvest /interval:30` - This command tells Rubeus to harvest for TGTs every 30 seconds  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_5.png" width="50%" height="50%">

### Brute-Forcing / Password-Spraying w/ Rubeus -
Rubeus can both brute force passwords as well as password spray user accounts. When brute-forcing passwords you use a single user account and a wordlist of passwords to see which password works for that given user account. In password spraying, you give a single password such as Password1 and "spray" against all found user accounts in the domain to find which one may have that password.  
This attack will take a given Kerberos-based password and spray it against all found users and give a .kirbi ticket. This ticket is a TGT that can be used in order to get service tickets from the KDC as well as to be used in attacks like the pass the ticket attack.  
Before password spraying with Rubeus, you need to add the domain controller domain name to the windows host file. You can add the IP and domain name to the hosts file from the machine by using the echo command:  
`echo 10.10.24.3 CONTROLLER.local >> C:\Windows\System32\drivers\etc\hosts`  
1.) cd Downloads - navigate to the directory Rubeus is in  
2.) `Rubeus.exe brute /password:Password1 /noticket` - This will take a given password and "spray" it against all found users then give the .kirbi TGT for that user  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_6.png" width="50%" height="50%">  
Be mindful of how you use this attack as it may lock you out of the network depending on the account lockout policies.

----------------------------------------Answer the questions below--------------------------------------------------  
`Rubeus`はWindows用のツールらしい（GitHubからソースコードをとってコンパイルして使わんといかん、メンディー）  
SSHでWindowsにログインして攻撃した。（RubeusはPost-Exploitation用っぽい）  
Which domain controller do we get a ticket for when harvesting tickets?  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_8.png" width="50%" height="50%">  
「`Rubeus.exe harvest /intercal:30`」で、30秒間のTGTチケット収集結果を確認すると、「CONTROLLER-1」が確認できた。  
Which domain admin do we get a ticket for when harvesting tickets?  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_7.png" width="50%" height="50%">  
同様に。「Administrator」がAdminとして確認できた。


## Kerberoasting w/ Rubeus & Impacket
﻿﻿In this task we'll be covering one of the most popular Kerberos attacks - Kerberoasting. Kerberoasting allows a user to request a service ticket for any service with a registered SPN then use that ticket to crack the service password. If the service has a registered SPN then it can be Kerberoastable however the success of the attack depends on how strong the password is and if it is trackable as well as the privileges of the cracked service account. To enumerate Kerberoastable accounts I would suggest a tool like BloodHound to find all Kerberoastable accounts, it will allow you to see what kind of accounts you can kerberoast if they are domain admins, and what kind of connections they have to the rest of the domain. That is a bit out of scope for this room but it is a great tool for finding accounts to target.  
In order to perform the attack, we'll be using both Rubeus as well as Impacket so you understand the various tools out there for Kerberoasting. There are other tools out there such a kekeo and Invoke-Kerberoast but I'll leave you to do your own research on those tools.  
I have already taken the time to put Rubeus on the machine for you, it is located in the downloads folder.

### Kerberoasting w/ Rubeus - 
1.) cd Downloads - navigate to the directory Rubeus is in  
2.) `Rubeus.exe kerberoast` This will dump the Kerberos hash of any kerberoastable users  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacking%20Kerberos_9.png" width="50%" height="50%">  
copy the hash onto your attacker machine and put it into a .txt file so we can crack it with hashcat  
I have created a modified rockyou wordlist in order to speed up the process download it [here](https://github.com/Cryilllic/Active-Directory-Wordlists/blob/master/Pass.txt)  
3.) `hashcat -m 13100 -a 0 hash.txt Pass.txt` - now crack that hash

### 
