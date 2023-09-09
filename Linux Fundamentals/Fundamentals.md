
The name "Linux" is actually an umbrella term for multiple OS's that are based on UNIX (another operating system)

|   |   |
|---|---|
|Command|Description|
|echo|Output any text that we provide|
|whoami|Find out what user we're currently logged in as!|

---

### FileSystem

|   |   |
|---|---|
|Command|Full Name|
|ls|listing|
|cd|change directory|
|cat|concatenate|
|pwd|print working directory|

Case insensitive find command

```sh
find / -iname vpn 2>/dev/null
```

/ : start searching from root directory recursively
iname: case insensitive

Find all files with the extension of txt in current folder

```sh
find -iname *.txt 2>/dev/null 
```

for case insensitive grep

```sh
ls | grep -i "shell"
```

to grep for specific extension 

```sh
ls | grep *.sh
```

grep in a file

```sh
grep "81.143.211.90" access.log
```

find the string inside file access.log


---

### Shell Operators

|   |   |
|---|---|
|Symbol / Operator|Description|
|&|This operator allows you to run commands in the background of your terminal.|
|&&|This operator allows you to combine multiple commands together in one line of your terminal.|
|>|This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere.|
|>>|This operator does the same function of the `>` operator but appends the output rather than replacing (meaning nothing is overwritten).|

```sh
command && command2
```

**command2 will only run if command 1 was successful**


---


**S**ecure **S**hell or **SSH** for short and is the common means of connecting to and interacting with the command line of a remote Linux machine.

##### How does SSH work?

Secure Shell or SSH simply is a protocol between devices in an encrypted form. Using cryptography, any input we send in a human-readable format is encrypted for travelling over a network -- where it is then unencrypted once it reaches the remote machine


![[Pasted image 20230908181113.png]]


- SSH allows us to remotely execute commands on another device remotely.
- Any data sent between the devices is encrypted when it is sent over a network such as the Internet


Information needed to login to a remote system

1. The IP address of the remote machine

2. Correct credentials to a valid account to login with on the remote machine


example: username=tryhackme, password=tryhackme

```sh
ssh tryhackme@10.10.82.232
```

Now that we are connected, any commands that we execute will now execute on the remote machine -- not our own.

---

### Flags and Switches

A majority of commands allow for arguments to be provided. These arguments are identified by a hyphen and a certain keyword known as flags or switches

Commands that accept these will also have a `--help` option. This option will list the possible options that the command accepts

```sh
ls -la
```

The manual pages are a great source of information for both system commands and applications available

To access this documentation, we can use the `man` command and then provide the command we want to read the documentation for.

```sh
man ls
```


---

### File System 2

|   |   |   |
|---|---|---|
|Command|Full Name|Purpose|
|touch|touch|Create file|
|mkdir|make directory|Create a folder|
|cp|copy|Copy a file or folder|
|mv|move|Move a file or folder|
|rm|remove|Remove a file or folder|
|file|file|Determine the type of a file|


mv command can also be used to rename a file

```sh
mv file newFile
```

file is renamed to newFile

remove files by using `rm`. However, you need to provide the `-R` switch alongside the name of the directory you wish to remove.

```sh
rm myFile
rm -r myDirectory
```

```sh
cp note note1
```

copy contents of note 1 to note 2


---

### Permissions

- Read : 4
- Write : 2
- Execute : 1

To switch to a different user

```sh
su userName
```

To become root user

```sh
sudo su
```


---

### Common Directories

The etc folder (short for etcetera) is a commonplace location to store system files that are used by your operating system.

The "/var" directory, with "var" being short for variable data,  is one of the main root folders found on a Linux install. This folder stores data that is frequently accessed or written by services or applications running on the system.

Unlike the **/home** directory, the **/root** folder is actually the home for the "root" system user. There isn't anything more to this folder other than just understanding that this is the home directory for the "root" user.

This is a unique root directory found on a Linux install. Short for "temporary", the /tmp directory is volatile and is used to store data that is only needed to be accessed once or twice. ***Similar to the memory on your computer, once the computer is restarted, the contents of this folder are cleared out.***
What's useful for us in pentesting is that any user can write to this folder by default. Meaning once we have access to a machine, it serves as a good place to store things like our enumeration scripts.

---

### Text Editors

```sh
nano filename
```

```sh
vim filename
```


---

### Downloading files

***wget*** command allows us to download files from the web via HTTP -- as if you were accessing the file in your browser.

```sh
wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt
```

##### Transferring Files From Your Host - SCP (Secure Copy Protocol)

***Secure copy, or SCP, is just that -- a means of securely copying files. Unlike the regular cp command, this command allows you to transfer files between two computers using the SSH protocol to provide both authentication and encryption.***

Working on a model of SOURCE and DESTINATION, SCP allows you to:

- Copy files & directories from your current system to a remote system
- Copy files & directories from a remote system to your current system


***Provided that we know usernames and passwords for a user on your current system and a user on the remote system***

**To copy a file from our machine to remote machine**

The IP address of the remote system : 192.168.1.30

User on the remote system : ubuntu

Name of the file on the local system : important.txt

Name that we wish to store the file as on the remote system : transferred.txt

```sh
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```


to copy a file from a remote computer that we're not logged into to our computer

IP address of the remote system : 192.168.1.30

User on the remote system : ubuntu

Name of the file on the remote system : documents.txt

Name that we wish to store the file as on our system : notes.txt


```sh
scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt
```

***the format of SCP is just SOURCE then DESTINATION***


To start a web server

```sh
python3 -m http.server 80
```

Start a http server on port 80

---

### Process

Processes are the programs that are running on your machine. They are managed by the kernel, where each process will have an ID associated with it, also known as its PID. The PID increments for the order In which the process starts. I.e. the 60th process will have a PID of 60.


`ps` command to provide a list of the running processes as our user's session and some additional information such as its status code, the session that is running it, how much usage time of the CPU it is using, and the name of the actual program or command that is being executed:

```sh
ps
```

To see the processes run by other users and those that don't run from a session (i.e. system processes), we need to provide **aux** to the `ps` command like so: `ps aux`

```sh
ps aux
```

```sh
top
```

- SIGTERM - Kill the process, but allow it to do some cleanup tasks beforehand
- SIGKILL - Kill the process - doesn't do any cleanup after the fact
- SIGSTOP - Stop/suspend a process

***The process with an ID of 0 is a process that is started when the system boots.***

`systemctl` -- this command allows us to interact with the **systemd** process/daemon.  systemctl is an easy to use command that takes the following formatting: `systemctl [option] [service]`

to tell apache to start up, we'll use `systemctl start apache2`

We can do four options with `systemctl`:

- Start
- Stop
- Enable : autostart on system boot-up
- Disable

Processes can run in two states: In the background and in the foreground.

---

Crontab is one of the processes that is started during boot, which is responsible for facilitating and managing cron jobs.

|   |   |
|---|---|
|Value|Description|
|MIN|What minute to execute at|
|HOUR|What hour to execute at|
|DOM|What day of the month to execute at|
|MON|What month of the year to execute at|
|DOW|What day of the week to execute at|
|CMD|The actual command that will be executed.|

