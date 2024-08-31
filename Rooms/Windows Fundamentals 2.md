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

----------------------------------------Answer the questions below--------------------------------------------------  
What is the command for Windows Troubleshooting?  
C:\Windows\System32\control.exe /name Microsoft.Troubleshooting
What command will open the Control Panel? (The answer is  the name of .exe, not the full path)  
control.exe ← コントロールパネルらしい


## Change UAC Settings
We're continuing with Tools that are available through the System Configuration panel.  
User Account Control (UAC) was covered in great detail in Windows Fundamentals 1.  
The UAC settings can be changed or even turned off entirely (not recommended).  
You can move the slider to see how the setting will change the UAC settings and Microsoft's stance on the setting.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_7.png" width="50%" height="50%">  

----------------------------------------Answer the questions below--------------------------------------------------  
What is the command to open User Account Control Settings? (The answer is the name of the .exe file, not the full path)  
UserAccountControlSettings.exe


## Computer Management
We're continuing with Tools that are available through the System Configuration panel.  
The Computer Management (`compmgmt`) utility has three primary sections: System Tools, Storage, and Services and Applications.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_8.png" width="50%" height="50%">

### System Tools
Let's start with Task Scheduler. Per Microsoft, with Task Scheduler, we can create and manage common tasks that our computer will carry out automatically at the times we specify.  
A task can run an application, a script, etc., and tasks can be configured to run at any point. A task can run at log in or at log off. Tasks can also be configured to run on a specific schedule, for example, every five mins.  
To create a basic task, click on Create Basic Task under Actions (right pane).  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_9.png" width="25%" height="25%">  
Next is Event Viewer.  
Event Viewer allows us to view events that have occurred on the computer. These records of events can be seen as an audit trail that can be used to understand the activity of the computer system. This information is often used to diagnose problems and investigate actions executed on the system.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_10.png" width="25%" height="25%">  
Event Viewer has three panes.
1. The pane on the left provides a hierarchical tree listing of the event log providers. (as shown in the image above)
2. The pane in the middle will display a general overview and summary of the events specific to a selected provider.
3. The pane on the right is the actions pane.

There are five types of events that can be logged. Below is a table from [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/eventlog/event-types) providing a brief description for each.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_11.png" width="50%" height="50%">  
The standard logs are visible under Windows Logs. Below is a table from [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/eventlog/eventlog-key) providing a brief description for each.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_12.png" width="50%" height="50%">  
For more information about Event Viewer and Event Logs, please refer to the Windows Event Log room.  
Shared Folders is where you will see a complete list of shares and folders shared that others can connect to.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_13.png" width="50%" height="50%">  
In the above image, under Shares, are the default share of Windows, C$, and default remote administration shares created by Windows, such as ADMIN$.  
As with any object in Windows, you can right-click on a folder to view its properties, such as Permissions (who can access the shared resource).  
Under Sessions, you will see a list of users who are currently connected to the shares. In this VM, you won't see anybody connected to the shares.  
All the folders and/or files that the connected users access will list under Open Files.  
The Local Users and Groups section you should be familiar with from Windows Fundamentals 1 because it's `lusrmgr.msc`.  
In Performance, you'll see a utility called Performance Monitor (`perfmon`).  
Perfmon is used to view performance data either in real-time or from a log file. This utility is useful for troubleshooting performance issues on a computer system, whether local or remote.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_14.png" width="50%" height="50%">  
Device Manager allows us to view and configure the hardware, such as disabling any hardware attached to the computer.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_15.png" width="50%" height="50%">  
