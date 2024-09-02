## Introduction
We will continue our journey exploring the Windows operating system.  
To summarize the previous two rooms:
- In Windows Fundamentals 1, we covered the desktop, the file system, user account control, the control panel, settings, and the task manager.
- In Windows Fundamentals 2, we covered various utilities, such as System Configuration, Computer Management, Resource Monitor, etc.

This module will attempt to provide an overview of the security features within the Windows operating system.


## Windows Updates
Let's start things off with Windows Update.  
Windows Update is a service provided by Microsoft to provide security updates, feature enhancements, and patches for the Windows operating system and other Microsoft products, such as Microsoft Defender.  
Updates are typically released on the 2nd Tuesday of each month. This day is called Patch Tuesday. That doesn't necessarily mean that a critical update/patch has to wait for the next Patch Tuesday to be released. If the update is urgent, then Microsoft will push the update via the Windows Update service to the Windows devices.  
Refer to the following link to see the Microsoft Security Update Guide [here](https://msrc.microsoft.com/update-guide).  
Windows Update is located in Settings. See below.  
Tip: Another way to access Windows Update is from the Run dialog box, or CMD, by running the command `control /name Microsoft.WindowsUpdate`.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_1.png" width="50%" height="50%">  
In the attached VM, there are a few things to highlight.  
1. The Windows Update settings are 'managed'. (Typically, home users will not see this type of message)
2. There are no available updates available for the virtual machine. (The attached virtual machine does not have Internet access to communicate with Microsoft to obtain new updates)
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_2.png" width="50%" height="50%">

Throughout the years, Windows users have grown accustomed to pushing Windows Updates off to a later date or not installing the updates at all. Various reasons caused this action, one being the fact that a reboot is typically required after a Windows update.  
Microsoft notably addressed this issue with Windows 10. The updates can no longer be ignored or pushed to the side until forgotten. Windows updates can only be postponed, but eventually, the update will happen, and your computer will reboot. Microsoft provides these updates to keep the device safe and secure.  
Below is an image showing how a Restart required looks and the several options available regarding scheduling the restart.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_3.png" width="50%" height="50%">
 
Refer to the Windows Updates [FAQ](https://support.microsoft.com/en-us/windows/windows-update-faq-8a903416-6f45-0718-f5c7-375e92dddeb2) for more information.


## Windows Security
Per Microsoft, "Windows Security is your home to manage the tools that protect your device and your data".  
In case you missed it, Windows Security is also available in Settings.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_4.png" width="50%" height="50%">  
In the above image, focus your attention on Protection areas.
- Virus & threat protection
- Firewall & network protection
- App & browser control
- Device security

Each following task will briefly touch on these areas.  
Before proceeding, let's provide a quick comment on the status icons.
- Green means your device is sufficiently protected, and there aren't any recommended actions.
- Yellow means there is a safety recommendation for you to review.
- Red is a warning that something needs your immediate attention.

Click on Open Windows Security.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_5.png" width="50%" height="50%">  
Note: Since the attached VM is a Windows Server 2019 edition, it looks different from a Windows 10 Home or Professional edition.  
The below image is from a Windows 10 device.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_6.png" width="35%" height="35%">  
Next, we'll look at Virus & threat protection.


## Virus & threat protection
Virus & threat protection is divided into two parts:
- Current threats
- Virus & threat protection settings

The image below only focuses on Current threats.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_7.png" width="35%" height="35%">

### Current threats
Scan options
- Quick scan - Checks folders in your system where threats are commonly found.
- Full scan - Checks all files and running programs on your hard disk. This scan could take longer than one hour.
- Custom scan - Choose which files and locations you want to check.

Threat history
- Last scan - Windows Defender Antivirus automatically scans your device for viruses and other threats to help keep it safe.
- Quarantined threats - Quarantined threats have been isolated and prevented from running on your device. They will be periodically removed.
- Allowed threats - Allowed threats are items identified as threats, which you allowed to run on your device.

Warning: Allow an item to run that has been identified as a threat only if you are 100% sure of what you are doing.  
Next is Virus & threat protection settings.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_8.png" width="35%" height="35%">

### Virus & threat protection settings
Manage settings 
- Real-time protection - Locates and stops malware from installing or running on your device.
- Cloud-delivered protection - Provides increased and faster protection with access to the latest protection data in the cloud.
- Automatic sample submission - Send sample files to Microsoft to help protect you and others from potential threats.
- Controlled folder access - Protect files, folders, and memory areas on your device from unauthorized changes by unfriendly applications.
- Exclusions - Windows Defender Antivirus won't scan items that you've excluded.
- Notifications - Windows Defender Antivirus will send notifications with critical information about the health and security of your device.

Warning: Excluded items could contain threats that make your device vulnerable. Only use this option if you are 100% sure of what you are doing.  
Virus & threat protection updates
- Check for updates - Manually check for updates to update Windows Defender Antivirus definitions.

Ransomware protection
- Controlled folder access - Ransomware protection requires this feature to be enabled, which in turn requires Real-time protection to be enabled.

Note: Real-time protection is turned off in the attached VM to decrease the chances of performance issues. Since the VM can't reach the Internet and there aren't any threats in the VM, this is safe to do. Real-time protection should definitely be enabled in your personal Windows devices unless you have a 3rd party product that provides the same protection. Ensure it's always up-to-date and enabled.  
Tip: You can perform on-demand scans on any file/folder by right-clicking the item and selecting 'Scan with Microsoft Defender'.  
The below image was taken from another Windows device to show this feature.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_9.png" width="25%" height="25%">


## Firewall & network protection
What is a firewall?  
Per Microsoft, "Traffic flows into and out of devices via what we call ports. A firewall is what controls what is - and more importantly isn't - allowed to pass through those ports. You can think of it like a security guard standing at the door, checking the ID of everything that tries to enter or exit".  
The below image will reflect what you will see when you navigate to Firewall & network protection.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_10.png" width="35%" height="35%">  
Note: Each network may have different status icons for you.  
What is the difference between the 3 (Domain, Private, and Public)?  
Per Microsoft, "Windows Firewall offers three firewall profiles: domain, private and public".
- Domain - The domain profile applies to networks where the host system can authenticate to a domain controller.
- Private - The private profile is a user-assigned profile and is used to designate private or home networks.
- Public - The default profile is the public profile, used to designate public networks such as Wi-Fi hotspots at coffee shops, airports, and other locations.

If you click on any firewall profile, another screen will appear with two options: turn the firewall on/off and block all incoming connections.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_11.png" width="35%" height="35%">  
Warning: Unless you are 100% confident in what you are doing, it is recommended that you leave your Windows Defender Firewall enabled.  
Allow an app through firewall  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_12.png" width="50%" height="50%">  
You can view what the current settings for any firewall profile are. In the above image, several apps have access in the Private and/or Public firewall profile. Some of the apps will provide additional information if it's available via the Details button.  
Advanced Settings  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_13.png" width="75%" height="75%">  
Configuring the Windows Defender Firewall is for advanced Windows users. Refer to the following Microsoft documentation on best practices [here](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-firewall/best-practices-configuring).  
Tip: Command to open the Windows Defender Firewall is `WF.msc`.


## App & browser control
In this section, you can change the settings for the Microsoft Defender SmartScreen.  
Per Microsoft, "Microsoft Defender SmartScreen protects against phishing or malware websites and applications, and the downloading of potentially malicious files".  
Refer to the official Microsoft document for more information on Microsoft Defender SmartScreen [here](https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview).  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_14.png" width="75%" height="75%">  

### Check apps and files
Windows Defender SmartScreen helps protect your device by checking for unrecognized apps and files from the web.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_15.png" width="75%" height="75%">  

### Exploit protection
Exploit protection is built into Windows 10 (and, in our case, Windows Server 2019) to help protect your device against attacks.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%203_16.png" width="75%" height="75%">  
Warning: Unless you are 100% confident in what you are doing, it is recommended that you leave the default settings. 
