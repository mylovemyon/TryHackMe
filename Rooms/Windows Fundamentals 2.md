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
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_8.png" width="25%" height="25%">

### System Tools
Let's start with Task Scheduler. Per Microsoft, with Task Scheduler, we can create and manage common tasks that our computer will carry out automatically at the times we specify.  
A task can run an application, a script, etc., and tasks can be configured to run at any point. A task can run at log in or at log off. Tasks can also be configured to run on a specific schedule, for example, every five mins.  
To create a basic task, click on Create Basic Task under Actions (right pane).  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_9.png" width="25%" height="25%">  
Next is Event Viewer.  
Event Viewer allows us to view events that have occurred on the computer. These records of events can be seen as an audit trail that can be used to understand the activity of the computer system. This information is often used to diagnose problems and investigate actions executed on the system.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_10.png" width="50%" height="50%">  
Event Viewer has three panes.
1. The pane on the left provides a hierarchical tree listing of the event log providers. (as shown in the image above)
2. The pane in the middle will display a general overview and summary of the events specific to a selected provider.
3. The pane on the right is the actions pane.

There are five types of events that can be logged. Below is a table from [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/eventlog/event-types) providing a brief description for each.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_11.png" width="75%" height="75%">  
The standard logs are visible under Windows Logs. Below is a table from [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/eventlog/eventlog-key) providing a brief description for each.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_12.png" width="75%" height="75%">  
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
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_15.png" width="25%" height="25%">  

### Storage
Under Storage is Windows Server Backup and Disk Management. We'll only look at Disk Management in this room.  
Note: Since the virtual machine is a Windows Server operating system, there are utilities available that you will typically not see in Windows 10.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_16.png" width="75%" height="75%">  
Disk Management is a system utility in Windows that enables you to perform advanced storage tasks.  Some tasks are:
- Set up a new drive
- Extend a partition
- Shrink a partition
- Assign or change a drive letter (ex. E:)

### Services and Applications
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_17.png" width="75%" height="75%">  
Recall from the previous task; a service is a special type of application that runs in the background. Here you can do more than enable and disable a service, such as view the Properties for the service.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_18.png" width="35%" height="35%">  

WMI Control configures and controls the Windows Management Instrumentation (WMI) service.  
Per Wikipedia, "WMI allows scripting languages (such as VBScript or Windows PowerShell) to manage Microsoft Windows personal computers and servers, both locally and remotely. Microsoft also provides a command-line interface to WMI called Windows Management Instrumentation Command-line (WMIC)."  
Note: The WMIC tool is deprecated in Windows 10, version 21H1. Windows PowerShell supersedes this tool for WMI.


## System Information
We're continuing with Tools that are available through the System Configuration panel.  
What is the System Information (`msinfo32`) tool?  
Per Microsoft, "Windows includes a tool called Microsoft System Information (Msinfo32.exe).  This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues."  
The  information in System Summary is divided into three sections:
- Hardware Resources
- Components
- Software Environment

System Summary will display general technical specifications for the computer, such as processor brand and model.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_19.png" width="75%" height="75%">  
The information displayed in Hardware Resources is not for the average computer user. If you want to learn more about this section, refer to the official Microsoft [page](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/hardware-resources#:~:text=Hardware%20resources%20are%20the%20assignable,of%20bus%2Drelative%20memory%20addresses.).  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_20.png" width="25%" height="25%">  
Under Components, you can see specific information about the hardware devices installed on the computer. Some sections don't show any information, but some sections do, such as Display and Input.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_21.png" width="15%" height="15%">  
In the Software Environment section, you can see information about software baked into the operating system and software you have installed. Other details are visible in this section as well, such as the Environment Variables and Network Connections.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_22.png" width="25%" height="25%">  
Recall from the Windows Fundamentals 1 room (The Windows\System32 Folder task) where Environment Variables was briefly touched on.  
Per [Microsoft](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.1), "Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders.  
The environment variables store data that is used by the operating system and other programs. For example, the WINDIR environment variable contains the location of the Windows installation directory. Programs can query the value of this variable to determine where Windows operating system files are located".  
Click on Environment Variables to see the assigned values for the virtual machine.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_23.png" width="75%" height="75%">  
Another method to view environment variables is Control Panel > System and Security > System > Advanced system settings > Environment Variables OR Settings > System > About > system info > Advanced system settings > Environment Variables.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_24.png" width="50%" height="50%">  
The detour is over. Let's redirect our attention back to msinfo32 and pick up where we left off.  
Towards the very bottom of this utility, there is a search bar. Please give it a go. Select Components and search for IP address.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_25.png" width="75%" height="75%">  


## Resource Monitor
We're continuing with Tools that are available through the System Configuration panel.  
What is Resource Monitor (`resmon`)?  
Per Microsoft, "Resource Monitor displays per-process and aggregate CPU, memory, disk, and network usage information, in addition to providing details about which processes are using individual file handles and modules. Advanced filtering allows users to isolate the data related to one or more processes (either applications or services), start, stop, pause, and resume services, and close unresponsive applications from the user interface. It also includes a process analysis feature that can help identify deadlocked processes and file locking conflicts so that the user can attempt to resolve the conflict instead of closing an application and potentially losing data."  
As some of the other tools mentioned in this room, this utility is geared primarily to advanced users who need to perform advanced troubleshooting on the computer system.  
In the Overview tab, Resmon has four sections:
- CPU
- Disk
- Network
- Memory

<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_26.png" width="75%" height="75%">  
The same four sections have corresponding tabs across the top. See below.  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_27.png" width="75%" height="75%">  
Note that each tab has additional information for each. An image is shown below for each tab.  
CPU  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_28.png" width="75%" height="75%">  
Memory  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_29.png" width="75%" height="75%">  
Disk  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_30.png" width="75%" height="75%">  
Network  
<img src="https://github.com/mylovemyon/TryHackMe_Images/blob/main/Images/Windows%20Fundamentals%202_31.png" width="75%" height="75%">  
Although not captured in any of the images above, Resource Monitor has a pane at the far right. This pane shows a graphical view in real-time for each section.  
Note: The information displayed in Resource Monitor will be different for you compared to the images above.


## 
