## System Configuration

The System Configuration utility `MSConfig` is for advanced troubleshooting, and its main purpose is to help diagnose startup issues. There are several methods to launch System Configuration. One method is from the Start Menu.
- The utility has five tabs across the top.
    1. General :- In the General tab, we can select what devices and services for Windows to load upon boot. The options are: Normal, Diagnostic, or Selective.
    2. Boot  :- In the Boot tab, we can define various boot options for the Operating System.
    3. Services :- The Services tab lists all services configured for the system regardless of their state (running or stopped). A service is a special type of application that runs in the background.
    4. Startup :- The Startup tab in System Configuration (MSConfig) is a feature that allows you to manage applications that run automatically when your computer starts.
    5. Tools :-  It allows users to launch specific tools directly from MSConfig, which can assist in managing system performance, diagnosing issues, or configuring settings.

## Computer Management 
The Computer Management `compmgmt` utility is a comprehensive administrative tool in Windows that organizes various system management features into three primary sections: System Tools, Storage, and Services and Applications.
1. System Tools: This section includes tools for managing user accounts, viewing event logs, and monitoring system performance. It allows administrators to manage local users and groups, access disk management settings, and review system event logs for troubleshooting.

2. Storage: In this section, users can manage disk partitions, format drives, and manage volumes. It provides an overview of the disks connected to the system and allows for disk management tasks like creating new partitions or resizing existing ones.

3. Services and Applications: This area allows users to manage Windows services and various applications. Administrators can start, stop, or configure services that run in the background, as well as manage applications that rely on these services.

## What is the System Information tool?

Windows includes a tool called Microsoft System Information `Msinfo32.exe`.  This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues.

## What is Resource Monitor?
Resource Monitor `resmon` displays per-process and aggregate CPU, memory, disk, and network usage information, in addition to providing details about which processes are using individual file handles and modules. Advanced filtering allows users to isolate the data related to one or more processes (either applications or services), start, stop, pause, and resume services, and close unresponsive applications from the user interface. It also includes a process analysis feature that can help identify deadlocked processes and file locking conflicts so that the user can attempt to resolve the conflict instead of closing an application and potentially losing data.

## System Configuration panel(command prompt)
The Command Prompt `cmd` is a command-line interface in Windows that allows users to execute commands directly
- Few simple commands, such as `hostname` and `whoami`:
    - The command `hostname` will output the computer name.
    - The command `whoami` will output the name of the logged-in user.
- A command used often is `ipconfig`. This command will show the network address settings for the computer.
- To clear the command prompt screen, the command is `cls`.
- The next command is `netstat` .  this command will display protocol statistics and current TCP/IP network connections.
- comprehensive list of commands you can execute in the command prompt [here](https://ss64.com/nt/).

## Windows Registry
The Windows Registry (per Microsoft) is a central hierarchical database used to store information necessary to configure the system for one or more users, applications, and hardware devices.
- The registry contains information that Windows continually references during operation, such as:
    - Profiles for each user
    - Applications installed on the computer and the types of documents that each can create
    - Property sheet settings for folders and application icons
    - ................
- There are various ways to view/edit the registry. One way is to use the Registry Editor `regedit`.
