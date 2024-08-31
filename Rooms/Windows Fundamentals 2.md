## Introduction
We will continue our journey exploring the Windows operating system.  
In Windows Fundamentals 1, we covered the desktop, the file system, user account control, the control panel, settings, and the task manager.  
This module will attempt to provide an overview of some other utilities available within the Windows operating system and different methods to access these utilities.


## System Configuration
The System Configuration utility (`MSConfig`) is for advanced troubleshooting, and its main purpose is to help diagnose startup issues.  
Reference the following document [here](https://docs.microsoft.com/en-us/troubleshoot/windows-client/performance/system-configuration-utility-troubleshoot-configuration-errors) for more information on the System Configuration utility.  
There are several methods to launch System Configuration. One method is from the Start Menu.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_1.png" width="50%" height="50%">  
Note: You need local administrator rights to open this utility.  
The utility has five tabs across the top. Below are the names for each tab. We will briefly cover each tab in this task.
- General
- Boot
- Services
- Startup
- Tools

<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_2.png" width="50%" height="50%">  
In the General tab, we can select what devices and services for Windows to load upon boot. The options are: Normal, Diagnostic, or Selective.  
In the Boot tab, we can define various boot options for the Operating System.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_3.png" width="50%" height="50%">  
The Services tab lists all services configured for the system regardless of their state (running or stopped). A service is a special type of application that runs in the background.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_4.png" width="50%" height="50%">  
In the Startup tab, you won't see anything interesting in the attached VM.  Below is a screenshot of the Startup tab for MSConfig from my local machine.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_5.png" width="50%" height="50%">

As you can see, Microsoft advises using Task Manager (`taskmgr`) to manage (enable/disable) startup items. The System Configuration utility is NOT a startup management program.  
Note: If you open Task Manager for the attached VM, you will notice that Task Manager doesn't show a Startup tab.  
There is a list of various utilities (tools) in the Tools tab that we can run to configure the operating system further. There is a brief description of each tool to provide some insight into what the tool is for.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_6.png" width="50%" height="50%">  
Notice the Selected command section. The information in this textbox will change per tool.  
To run a tool, we can use the command to launch the tool via the run prompt, command prompt, or by clicking the Launch button. 
