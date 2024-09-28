## Introduction
A computer network is a group of computers and devices connected with each other. Network security focuses on protecting the security of these devices and the links connecting them. (In more precise terms, network security refers to the devices, technologies, and processes to protect the confidentiality, integrity, and availability of a computer network and the data on it.)  
Network security consists of different hardware and software solutions to achieve the set security goals. Hardware solutions refer to the devices you set up in your network to protect your network security. They are hardware, so you can literally hold them. A hardware appliance might look something like the image below.  
Examples of hardware appliances include:  
- Firewall appliance: The firewall allows and blocks connections based on a predefined set of rules. It restricts what can enter and what can leave a network.
- Intrusion Detection System (IDS) appliance: An IDS detects system and network intrusions and intrusion attempts. It tries to detect attackers’ attempts to break into your network.
- Intrusion Prevention System (IPS) appliance: An IPS blocks detected intrusions and intrusion attempts. It aims to prevent attackers from breaking into your network.
- Virtual Private Network (VPN) concentrator appliance: A VPN ensures that the network traffic cannot be read nor altered by a third party. It protects the confidentiality (secrecy) and integrity of the sent data.

On the other hand, we have software security solutions. Common examples are:
- Antivirus software: You install an antivirus on your computer or smartphone to detect malicious files and block them from executing.
- Host firewall: Unlike the firewall appliance, a hardware device, a host firewall is a program that ships as part of your system, or it is a program that you install on your system. For instance, MS Windows includes Windows Defender Firewall, and Apple macOS includes an application firewall; both are host firewalls.

According to the [Cost of a Data Breach Report 2021](https://newsroom.ibm.com/2021-07-28-IBM-Report-Cost-of-a-Data-Breach-Hits-Record-High-During-Pandemic) by IBM Security, a data breach in 2021 cost a company $4.24 million per incident on average, in comparison with $3.86 million in 2020. The average cost changes with the sector and the country. For example, the average total cost for a data breach was $9.23 million for the healthcare sector, while $3.79 million for the education sector.


## Methodology
Every “operation” requires some form of planning to achieve success. If you are interested in wildlife photography, you cannot just grab a camera and head to the jungle unless you don’t care about the outcome. For a safe and successful wildlife photography tour, you would need to learn more about the animals you want to shoot with your camera. This includes the habits of the animals and the dangers to avoid. The same would apply to a military operation against a target or breaking into a target network.
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Network%20Security_1.png" width="50%" height="50%">  
Breaking into a target network usually includes a number of steps. According to [Lockheed Martin](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html), the Cyber Kill Chain has seven steps:  
1. Recon: Recon, short for reconnaissance, refers to the step where the attacker tries to learn as much as possible about the target. Information such as the types of servers, operating system, IP addresses, names of users, and email addresses, can help the attack’s success.
2. Weaponization: This step refers to preparing a file with a malicious component, for example, to provide the attacker with remote access.
3. Delivery: Delivery means delivering the “weaponized” file to the target via any feasible method, such as email or USB flash memory.
4. Exploitation: When the user opens the malicious file, their system executes the malicious component.
5. Installation: The previous step should install the malware on the target system.
6. Command & Control (C2): The successful installation of the malware provides the attacker with a command and control ability over the target system.
7. Actions on Objectives: After gaining control over one target system, the attacker has achieved their objectives. One example objective is Data Exfiltration (stealing target’s data).

Another analogy would be a thief interested in a target house. The thief will spend some time learning about the target house, who lives there, when they leave, and when they return home. The thief will determine whether they have security cameras and alarm systems. Once enough information has been gathered, the thief will plan the best entrance strategy. Physical theft planning and execution resemble, in a way, the malicious attack that aims to break into a network and steal data.  
In the next task, we will carry out a practical example of the Cyber Kill Chain.


## Practical Example of Network Security
The first step of our attack is `Recon`; we can speed up our reconnaissance activities using different tools that gather information about the various aspects related to the target. For simplicity, we will use a single tool in this task, Nmap, short for Network Mapper. Nmap is a network scanner that helps us discover running machines and any programs running on them that are visible to the outside world. The IP address of the target is MACHINE_IP. We can scan it by running nmap MACHINE_IP at the terminal prompt.  
```
root@AttackBox# nmap MACHINE_IP
Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-06 17:38 EEST
Nmap scan report for 10.20.30.130
Host is up (0.00024s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.33 seconds
```
We just discovered three services running:
1. FTP server: FTP stands for File Transfer Protocol and is used to transfer files between machines.
2. SSH server: SSH stands for Secure Shell and is used for secure remote login. In other words, it allows you to execute commands on a remote system securely.
3. HTTP server: HTTP stands for Hypertext Transfer Protocol and is used for the web. Whenever you are browsing the web, you are using HTTP or HTTPS. HTTPS is the secure (encrypted) version of HTTP.

You can also notice that Nmap reports on whether the host is up based on whether it receives any response from it. This is useful to know when no ports are open or accessible.  
Let’s try to gather more information about the FTP server.
1. We will connect to the target FTP server by typing on the AttackBox’s terminal `ftp MACHINE_IP`.
2. Next, we will try to log in using the login `anonymous` to see if this FTP server supports anonymous logins. To our luck, it worked.
3. We try to see the files available using the command `ls`, short for list. We get a list of the filenames along with their details.
4. If you are curious about any file, you can download it using `get filename`. I wonder what the file `secret.txt` contains, so let’s download it using `get secret.txt`.
5. Once you download the files, type `exit` or `bye` to quit the FTP client.

The above interaction with the FTP server is shown in the terminal output below.
```
root@AttackBox# ftp MACHINE_IP
Connected to MACHINE_IP (MACHINE_IP).
220 (vsFTPd 3.0.3)
Name (MACHINE_IP:root): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
227 Entering Passive Mode (10,20,30,130,181,190).
150 Here comes the directory listing.
-rw-r--r--    1 ftp      ftp        425351 Apr 06 11:22 2680-0.txt
-rw-r--r--    1 ftp      ftp           356 Apr 06 11:22 2680.epub
-rw-r--r--    1 ftp      ftp        251857 Apr 06 11:22 55317-0.txt
-rw-r--r--    1 ftp      ftp           358 Apr 06 11:22 55317.epub
-rwxr-xr-x    1 ftp      ftp           214 Apr 06 11:22 backup.sh
-rw-r--r--    1 ftp      ftp            23 Apr 06 11:22 secret.txt
226 Directory send OK.
ftp> get secret.txt 
local: secret.txt remote: secret.txt
227 Entering Passive Mode (10,20,30,130,159,46).
150 Opening BINARY mode data connection for secret.txt (23 bytes).
226 Transfer complete.
23 bytes received in 0.00107 secs (21.48 Kbytes/sec)
ftp> exit
221 Goodbye.
```
Looking at the files, we notice six files: three txt files, two epub files, and one sh file. The first two extensions are for text files and ebooks, while the sh extension indicates that the file is a shell script. A shell script usually contains a group of commands that needs to be performed repetitively.  
After we downloaded the file secret.txt with the FTP command `get secret.txt` and exited the FTP client using exit, we returned to the terminal. Let’s display the contents of the file secret.txt using `cat secret.txt`.  
```
root@AttackBox# cat secret.txt 
password: [redacted]
```
We have kept the password hidden so you can try it for yourself. Repeat the above steps till you can display the contents of secret.txt and use it to answer the first question in this task.  
It must be the password of one of the accounts unintentionally copied to a public FTP server. Let’s try it to see if it works with the root account. The root account has full privileges on a Linux system, meaning that it can read and write any file and install and remove any program. At the terminal, we type `ssh root@MACHINE_IP`. We will be asked for the password, so let’s try the password we discovered in the FTP server.  
```
root@AttackBox# ssh root@MACHINE_IP
root@MACHINE_IP's password: 
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-107-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu  7 Apr 08:16:42 UTC 2022

  System load:  0.15              Processes:              225
  Usage of /:   64.6% of 6.53GB   Users logged in:        0
  Memory usage: 19%               IPv4 address for ens33: MACHINE_IP
  Swap usage:   0%

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

0 updates can be applied immediately.


Last login: Thu Apr  7 07:53:28 2022 from 10.10.10.1
```
Congratulations! You now have complete control over the target server. Let’s collect a couple of flags. After logging in as `root`, we used the following Linux commands:  
1. `pwd`, short for print working directory, to see where we are in the system. We are in the `/root` directory.
2. `ls` to list the files. We notice a flag.txt.
3. Use `cat flag.txt` to answer the second question in this task.
```
root@AttackBox# pwd
/root
root@AttackBox# ls
flag.txt  snap
root@AttackBox# cat flag.txt 
[redacted]
```
Because we are logged in as root, we have full access to all files, including other users’ files. Let’s try this out. We executed the following Linux commands:  
1. `cd /home` to go to the directory containing all the users’ home directories. `cd` is short for change directory.
2. We run `ls` while in `/home`. We notice `librarian` is one of the users on the system. However, we have system administrator (`root`) privileges to check the contents of his home folder.
3. `cd librarian` to go to the user’s directory.
4. `pwd` to confirm that we are at `/home/librarian`.
5. `ls` shows that `librarian` has a single file `flag.txt`.
6. We can print the text file contents using `cat flag.txt. Use this to answer the third question in this task.
```
root@AttackBox# cd /home
root@AttackBox# ls
ftpsecure  librarian  strategos
root@AttackBox# cd librarian/
root@AttackBox# pwd
/home/librarian
root@AttackBox# ls
flag.txt
root@AttackBox# cat flag.txt 
[redacted]
```
Let’s summarize what we have done in this task to get `root` access on the target system of IP address MACHINE_IP:  
1. We used `nmap` to learn about the running services.
2. We connected to the FTP server to learn more about its configuration.
3. We discovered a file containing the root password mistakenly copied to a public folder.
4. We used the password we found, allowing us to log in successfully.
5. We gained access to all the users’ files.

----------------------------------------Answer the questions below--------------------------------------------------  
What is the password in the secret.txt file?  
What is the content of the flag.txt in the /root directory?  
What is the content of the flag.txt in the /home/librarian directory?  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Network%20Security_2.png" width="40%" height="40%">
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Network%20Security_3.png" width="40%" height="40%">  
上記の要領と同じように「`ftp IPアドレス -a`」でAnonymousログオンでRootパスワード発見、SSHログインでフラグを発見
