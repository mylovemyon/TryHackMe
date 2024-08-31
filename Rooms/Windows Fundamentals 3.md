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
