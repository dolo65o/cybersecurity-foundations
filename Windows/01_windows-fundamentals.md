## File system

The on-disk data structures and logic an OS uses to organise, name, store and retrieve files (e.g. FAT32, NTFS, ext4).The file system used in modern versions of  Windows  is the New Technology File System or simply  NTFS .Before NTFS, there was  FAT16/FAT32 (File Allocation Table) and HPFS (High Performance File System).
- NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT.
- Microsoft's official documentation on FAT, HPFS, and NTFS [here](https://docs.microsoft.com/en-us/troubleshoot/windows-client/backup-and-storage/fat-hpfs-and-ntfs-file-systems) .

- On NTFS volumes, you can set permissions that grant or deny access to files and folders.
    - The permissions are:
      - Full control
      - Modify
      - Read & Execute
      - List folder contents
      - Read
      - Write

- Another feature of NTFS is Alternate Data Streams ( ADS ).
    - Alternate Data Streams  (ADS) is a file attribute specific to Windows  NTFS  (New Technology File System).
    - Every file has at least one data stream `( $DATA )`, and ADS allows files to contain more than one stream of data. Natively Window Explorer doesn't display ADS to the user. There are 3rd party executables that can be used to view this data, PowerShell also gives you the ability to view ADS for files.

## Environment Variable
Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders.
- Used by applications and the OS at runtime
- Examples:
    - `%windir%`  → Windows directory
    - `%temp%`   → Temporary files location
    - `%path%`   → Executable search paths

## Windows User Accounts & Profiles
Windows has two main local user account types:
1. Administrator
   - Can:
      - install/uninstall software
      - add or remove users
      - change system-wide settings
      - manage groups and permissions
2. Standard User
   - Can:
      - access own files and folders
      - use installed applications

## Local Users and Groups Management

- This console allows administrators to manage user accounts and groups on a local computer.
- Command : `lusrmgr.msc`

## User Account Control (UAC)
User Account Control (UAC) helps prevent malware from damaging a PC and helps organizations deploy a better-managed desktop. With UAC, apps and tasks always run in the security context of a non-administrator account, unless an administrator specifically authorizes administrator-level access to the system. UAC can block the automatic installation of unauthorized apps and prevent inadvertent changes to system settings.
> more about [UAC](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/how-it-works) here

