##  Deploy The Machine


##  Setup
### Installing Impacket:
Whether you're on the Kali 2019.3 or Kali 2021.1, Impacket can be a pain to install  correctly. Here's some instructions that may help you install it correctly!  
Note: All of the tools mentioned in this task are installed on the AttackBox already. These steps are only required if you are setting up on your own VM. Impacket may also need you to use a python version >=3.7. In the AttackBox you can do this by running your command with python3.9 <your command>.

First, you will need to clone the Impacket Github repo onto your box. The following command will clone Impacket into /opt/impacket:  
`git clone https://github.com/SecureAuthCorp/impacket.git /opt/impacket`  
After the repo is cloned, you will notice several install related files, requirements.txt, and setup.py. A commonly skipped file during the installation is setup.py, this actually installs Impacket onto your system so you can use it and not have to worry about any dependencies.  
To install the Python requirements for Impacket:  
`pip3 install -r /opt/impacket/requirements.txt`  
Once the requirements have finished installing, we can then run the python setup install script:  
`cd /opt/impacket/ && python3 ./setup.py install`  
After that, Impacket should be correctly installed now and it should be ready to use!  
Credit for proper Impacket install instructions goes to Dragonar#0923 in the THM [Discord](https://discord.gg/tryhackme) <3

### Installing Bloodhound and Neo4j
Bloodhound is another tool that we'll be utilizing while attacking Attacktive Directory. We'll cover specifcs of the tool later, but for now, we need to install two packages with Apt, those being bloodhound and neo4j. You can install it with the following command:  
`apt install bloodhound neo4j`  
 Now that it's done, you're ready to go!  

 ### Troubleshooting
If you are having issues installing Bloodhound and Neo4j, try issuing the following command:  
`apt update && apt upgrade`  
If you are having issues with Impacket, reach out to the TryHackMe Discord for help!

impacketはKaliでは、`/usr/share/doc/python3-impacket/examples`内にデフォルトであった（パスも通ってる）  
bloodhoundはないので、`sudo apt install bloodhound`でインストール（自動でneo4jもインストールしてくれる）


## Welcome to Attacktive Directory
### Welcome to Attacktive Directory
Welcome Dear User!  
Thank you for doing my first room. I originally created this room for my final project in my Cyber Security degree program back in 2019. Since then, I've gone on to make several other rooms, even a Network for THM. In May 2021, I made the decision to renovate this room and make it more guided and less challenge based so there are more learning opportunities for others. I hope you enjoy it.  
Love,
[Spools](https://twitter.com/NekoS3c)

### Enumeration
Basic enumeration starts out with an nmap scan. Nmap is a relatively complex utility that has been refined over the years to detect what ports are open on a device, what services are running, and even detect what operating system is running. It's important to note that not all services may be deteted correctly and not enumerated to it's fullest potential. Despite nmap being an overly complex utility, it cannot enumerate everything. Therefore after an initial nmap scan we'll be using other utilities to help us enumerate the services running on the device.  
For more information on nmap, check out the [nmap room](https://tryhackme.com/room/furthernmap).
Notes: Flags for each user account are available for submission. You can retrieve the flags for user accounts via RDP (Note: the login format is spookysec.local\User at the Window's login prompt) and Administrator via Evil-WinRM.

----------------------------------------Answer the questions below--------------------------------------------------  
What is the NetBIOS-Domain Name of the machine?  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacktive%20Directory_1.png" width="50%" height="50%">  
`enum4linux IPアドレス`でスキャンして確認できた。  

What invalid TLD do people commonly use for their Active Directory Domain?  
`.local`


##  Enumerating Users via Kerberos
### Introduction:  
A whole host of other services are running, including Kerberos. Kerberos is a key authentication service within Active Directory. With this port open, we can use a tool called [Kerbrute](https://github.com/ropnop/kerbrute/releases) (by Ronnie Flathers @ropnop) to brute force discovery of users, passwords and even password spray!  
Note: Several users have informed me that the latest version of Kerbrute does not contain the UserEnum flag in Kerbrute, if that is the case with the version you have selected, try a older version!

### Enumeration:
For this box, a modified [User List](https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/master/userlist.txt) and [Password List](https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/master/passwordlist.txt) will be used to cut down on time of enumeration of users and password hash cracking. It is NOT recommended to brute force credentials due to account lockout policies that we cannot enumerate on the domain controller.

----------------------------------------Answer the questions below--------------------------------------------------  
What notable account is discovered?   
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacktive%20Directory_2.png" width="50%" height="50%">  
Nmapで3389が開いているのを確認したため、`-sC`でスクリプトスキャンするとドメインを確認できた。  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacktive%20Directory_3.png" width="50%" height="50%">  
[User List](https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/master/userlist.txt)をWgetして「`./kerbrute userenum -d ドメイン名 --dc ドメコンIP Wordlists名`」でドメイン内のユーザを発見できる。  
wordlistは70000以上あったのでめっちゃ時間かかるので、途中で中断。  
問題で聞かれている怪しいユーザは、svc-admin と backup らしい。


## Abusing Kerberos
### Introduction
After the enumeration of user accounts is finished, we can attempt to abuse a feature within Kerberos with an attack method called `ASREPRoasting`. ASReproasting occurs when a user account has the privilege "Does not require Pre-Authentication" set. This means that the account does not need to provide valid identification before requesting a Kerberos Ticket on the specified user account.

### Retrieving Kerberos Tickets
[Impacket](https://github.com/fortra/impacket) has a tool called "GetNPUsers.py" (located in impacket/examples/GetNPUsers.py) that will allow us to query ASReproastable accounts from the Key Distribution Center. The only thing that's necessary to query accounts is a valid set of usernames which we enumerated previously via Kerbrute.  
Remember:  Impacket may also need you to use a python version >=3.7. In the AttackBox you can do this by running your command with `python3.9 /opt/impacket/examples/GetNPUsers.py`.

----------------------------------------Answer the questions below--------------------------------------------------  
We have two user accounts that we could potentially query a ticket from. Which user account can you query a ticket from with no password?  
`svc-admin`が怪しいらしい。  
Now crack the hash with the modified password list provided, what is the user accounts password?  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacktive%20Directory_4.png" width="100%" height="100%">  
`python3 /usr/share/doc/python3-impacket/examples/GetNPUsers.py -format john -no-pass -dc-ip ドメコンIP ドメイン名/ユーザ名`で
事前認証(AS-req)が無効であるユーザのTGTチケットを取得することができた。  
その後、 [Password List](https://raw.githubusercontent.com/Sq00ky/attacktive-directory-tools/master/passwordlist.txt)をWgetして、Johnでクラック成功！


## Back to the Basics
### Enumeration:
With a user's account credentials we now have significantly more access within the domain. We can now attempt to enumerate any shares that the domain controller may be giving out.

----------------------------------------Answer the questions below--------------------------------------------------  
What utility can we use to map remote SMB shares?  
There is one particular share that we have access to that contains a text file. Which share is it?  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacktive%20Directory_5.png" width="75%" height="75%">  
「`smbclient -L IPアドレス or FQDN -U ユーザ名%パスワード`」でShareを列挙できる。（-Lオプション）  
「`smbclient //IPアドレス/共有名 -U ユーザ名%パスワード`」で共有にアクセス、怪しいファイルを発見・ダウンロードできた。  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacktive%20Directory_6.png" width="50%" height="50%">  
ちなみに「`smbmap -H IPアドレス -u ユーザ名 -p パスワード`」でもShareの列挙ができる。  
Decoding the contents of the file, what is the full contents?  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Attacktive%20Directory_7.png" width="75%" height="75%">  
