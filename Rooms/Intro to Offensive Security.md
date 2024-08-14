## What is Offensive Security?
In short, offensive security is the process of breaking into computer systems, exploiting software bugs, and finding loopholes in applications to gain unauthorized access to them.  
To beat a hacker, you need to behave like a hacker, finding vulnerabilities and recommending patches before a cybercriminal does, as you'll do in this room!  
On the flip side, there is also defensive security, which is the process of protecting an organization's network and computer systems by analyzing and securing any potential digital threats; learn more in the digital forensics room.  
In a defensive cyber role, you could be investigating infected computers or devices to understand how it was hacked, tracking down cybercriminals, or monitoring infrastructure for malicious activity.

## Hacking your first machine
Before going into cyber security careers and what offensive security is, let's get you hacking (and yes, its legal, all exercises are fake simulations)  
We will use a command-line application called "GoBuster" to brute-force FakeBank's website to find hidden directories and pages. GoBuster will take a list of potential page or directory names and tries accessing a website with each of them; if the page exists, it tells you.  
Step 1) Open a terminal  
A terminal, also known as the command-line, allows us to interact with a computer without using a graphical user interface. On the machine, open the terminal using the Terminal icon:  
Step 2) Find hidden website pages  
Most companies will have an admin portal page, giving their staff access to basic admin controls for day-to-day operations. For a bank, an employee might need to transfer money to and from client accounts. Often these pages are not made private, allowing attackers to find hidden pages that show, or give access to, admin controls or sensitive data.  
Type the following command into the terminal to find potentially hidden pages on FakeBank's website using GoBuster (a command-line security application).  
`gobuster -u http://fakebank.com -w wordlist.txt dir`  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Intro%20to%20Offensive%20Security_1.png" width="50%" height="50%">  
In the command above, `-u` is used to state the website we're scanning, `-w` takes a list of words to iterate through to find hidden pages.  
You will see that GoBuster scans the website with each word in the list, finding pages that exist on the site. GoBuster will have told you the pages it found in the list of page/directory names (indicated by Status: 200).  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Intro%20to%20Offensive%20Security_2.png" width="50%" height="50%">  
Step 3) Hack the bank  
You should have found a secret bank transfer page that allows you to transfer money between accounts at the bank (/bank-transfer). Type the hidden page into the FakeBank website on the machine.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Intro%20to%20Offensive%20Security_3.mp4" width="50%" height="50%">  
