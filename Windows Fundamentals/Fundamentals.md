The Windows Desktop, aka the graphical user interface or GUI in short, is the screen that welcomes you once you log into a Windows 10 machine

The file system used in modern versions of Windows is the New Technology File System or simply NTFS. 

Before NTFS, there was **FAT16/FAT32** (File Allocation Table) and **HPFS** (High Performance File System).

FAT partitions in USB devices, MicroSD cards, etc. but traditionally not on personal Windows computers/laptops or Windows servers.
NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT.

NTFS addresses many of the limitations of the previous file systems; such as: 

    Supports files larger than 4GB
    Set specific permissions on folders and files
    Folder and file compression
    Encryption (Encryption File System or EFS)

The Windows folder (`C:\Windows`) is traditionally known as the folder which contains the Windows operating system.

This is where environment variables, more specifically system environment variables, come into play.
the system  environment variable for the Windows directory is `%windir%`.

Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders

***The System32 folder holds the important files that are critical for the operating system.***

User accounts can be one of two types on a typical local Windows system: **Administrator** & **Standard User**.

The user account type will determine what actions the user can perform on that specific Windows system. 

- An Administrator can make changes to the system: add users, delete users, modify groups, modify settings on the system, etc. 
- A Standard User can only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.

To protect the local user with such privileges, Microsoft introduced **User Account Control** (UAC).

UAC (by default) doesn't apply for the built-in local administrator account.

How does UAC work? When a user with an account type of administrator logs into a system, the current session doesn't run with elevated permissions. When an operation requiring higher-level privileges needs to execute, the user will be prompted to confirm if they permit the operation to run.

Command Prompt

whoami 
hostname 
ipconfig
ipconfig /all
netstat
cls : clear screen

