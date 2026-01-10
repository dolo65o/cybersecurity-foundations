## What is SSH & how Does it Work?

Secure Shell or SSH simply is a protocol between devices in an encrypted form. Using cryptography, any input we send in a human-readable format is encrypted for travelling over a network -- where it is then unencrypted once it reaches the remote machine.
- SSH allows us to remotely execute commands on another device remotely.
- Any data sent between the devices is encrypted when it is sent over a network such as the Internet.

## Using SSH to Login to Your Linux Machine
The syntax to use SSH is very simple. We only need to provide two things:
1. The IP address of the remote machine
2. Correct credentials to a valid account to login with on the remote machine

> For example: ssh tryhackme@MACHINE_IP

## Flags or Switches

In command-line interfaces, many commands accept additional inputs known as arguments. These arguments are often prefixed with a hyphen `-` and are referred to as flags or switches. They modify the behavior of the command, allowing users to specify options that tailor the command's functionality to their needs. For example, in a command like ls, the `-l` flag can be used to display a detailed list of files, while `-a` might show hidden files.

> Commands that accept these will also have a `--help` option. This option will list the possible options that the command accepts, provide a brief description and example of how to use it.

## The Man(ual) Page

The manual pages are a great source of information for both system commands and applications available on both a Linux machine, which is accessible on the machine itself and [online](https://linux.die.net/man/).

- To access this documentation, we can use the `man` command and then provide the command we want to read the documentation for. Using our `ls` example, we would use `man ls` to view the manual pages for `ls` like so:
```
tryhackme@linux2:~$ man ls
LS(1)                                               User Commands                                               LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List  information  about the FILEs (the current directory by default).  Sort entries alphabetically if none of
       -cftuvSUX nor --sort is specified.

       Mandatory arguments to long options are mandatory for short options too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..

       --author
              with -l, print the author of each file

       -b, --escape
              print C-style escapes for nongraphic characters

       --block-size=SIZE
              with -l, scale sizes by SIZE when printing them; e.g., '--block-size=M'; see SIZE format below

 Manual page ls(1) line 1 (press h for help or q to quit)

```

## File & Directory Management Commands

| Command | Full Name | Purpose | Example |
|------|-----------|--------|--------|
| `touch` | touch | Create an empty file | `touch file.txt` |
| `mkdir` | make directory | Create a directory | `mkdir test_folder` |
| `cp` | copy | Copy a file or directory | `cp file.txt backup.txt` |
| `mv` | move | Move or rename a file | `mv file.txt newfile.txt` |
| `rm` | remove | Delete a file or directory | `rm file.txt` |
| `file` | file | Identify file type | `file file` |

> The '-R' switch in the context of the 'rm' command is used to remove directories and their contents recursively. When you want to delete a directory that may contain files and subdirectories, you must specify the '-R' option to ensure that all nested files and folders are removed as well. For example, using 'rm -R mydirectory' will delete 'mydirectory' along with everything inside it.

## The Differences Between Users & Groups

In Linux, files and directories have ownership and permission settings that determine access. Every file is owned by a user and a group. The owner has specific permissions (read, write, execute) that dictate what actions they can perform on the file. Meanwhile, groups can have distinct permissions, allowing multiple users to share access levels without changing the file's ownership. 

### Switching Between Users

With the help of `su` command we can switch multiple User Unless you are the root user (or using root permissions through sudo),if you are then, you need Password and username .
- `su` command also work with ouple of switches
    - e.g :- `-l` or `--login`

EXAMPLE :- 
```
tryhackme@linux2:~$ su user2
Password:
user2@linux2:/home/tryhackme$
```
> when using su to switch to "user2", our new session drops us into our previous user's home directory.

```
tryhackme@linux2:~$ su -l user2
Password:
user2@linux2:~$ pwd
user2@:/home/user2$
```
> Where now, after using `-l`, our new session has dropped us into the home directory of "user" automatically.

## Common Directories

1. `/etc` Directory
  - The `/etc` directory is one of the most important system directories in Linux. Meaning `/etc` stores system-wide configuration files.
  - These files control:
      - users
      - passwords
      - permissions
      - services
  - Changes here affect the entire system
  - Only root (administrator) can modify most files in `/etc`.

2. `/var` Directory
   - The `/var` directory stores variable data — data that changes frequently. Meaning Used by running services and applications,Data grows, updates, and rotates over time.

3. `/root` Directory
   - `/root` is the home directory of the root user.
   - Normal users cannot access this directory.
   - Stores files and folders belonging to the root user.
   - Used for:
      - administrative scripts
      - sensitive files
      - system-level tasks

4. `/tmp` Directory
   - `/tmp` stands for temporary.
   - Used to store short-lived files
   - Contents are usually cleared after reboot
