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

impacketはKali上でFindしてみると何個かあったのでデフォルトであるっぽい？
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
