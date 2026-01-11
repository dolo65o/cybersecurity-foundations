## Terminal Text Editors

**Nano**
- To create or edit a file using nano, we simply use nano filename.
- Nano has a few features that are easy to remember:-
    - Searching for text
    - Copying and Pasting
    - Jumping to a line number
    - Finding out what line number you are on

**VIM**

VIM is a much more advanced text editor. Whilst you're not expected to know all advanced features, it's helpful to mention it for powering up your Linux skills.

- Some of VIM's benefits:-
    - you can modify the keyboard shortcuts to be of your choosing
    - Syntax Highlighting
    - VIM works on all terminals where nano may not be installed
    - There are a lot of resources such as [cheatsheets](https://vim.rtorr.com/).

## File Transfer in Linux 

1. Downloading Files using `wget`
   - wget is used to download files from the internet using a URL.
   - Example:-
       - `wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt`
   - Explanation:-
       - The system connects to the web server
       - Requests the file
       - Downloads and saves it in the current directory
> `wget` does NOT need username or password (unless the file is protected).

2. Transferring Files using `scp` (Secure Copy)
   - `scp` is used to securely copy files between two computers using `SSH`. Data is encrypted during transfer.
   - Rule:-
       - `scp SOURCE DESTINATION `
   - This works on both ways remote to local system or local to remote system.
   - Example:-` scp <local_file> <user>@<IP>:<remote_path>` Means `scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt`
   - AND :- `scp <user>@<IP>:<remote_file> <local_file>` Means `scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt`
> `scp` always asks for the remote user’s password.

3. Serving Files using Python Web Server
  - Python can be used to turn your machine into a temporary web server. Other machines can download files from it using `wget` or `curl`.
  - Command to start web server :- `python3 -m http.server`
  - Server starts on port 8000.
  - Terminal must stay open while server is running.

4. Downloading Files from the Python Web Server
  - will need to run the `wget` command in another terminal (while keeping the terminal that is running the Python3 server active).
  - Example:-`wget http://10.49.142.254:8000/file`

## WHAT IS A PROCESS?
- A process = a program that is currently running.
- When we run a command → a process is created
- Linux kernel manages all processes
- Every process gets a PID (Process ID)
    - Example: PID 204, 205, etc.
- PID always increases as new processes start.

1. Viewing Processes – `ps`
  - `ps` command to provide a list of the running processes as our user's session and some additional information such as its status code, the session that is running it, how much usage time of the CPU it is using, and the name of the actual program or command that is being executed.
  - `ps` itself becomes a process (that’s why PID changes each time).
  - **`ps aux`** :- To see the processes run by other users and those that don't run from a session (i.e. system processes), we need to provide aux to the `ps` command like so: `ps aux`.

2. Real-time Process Monitoring – `top`
  - `top` gives you real-time statistics about the processes running on your system instead of a one-time view. These statistics will refresh every 10 seconds, but will also refresh when you use the arrow keys to browse the various rows.

3. Managing (Killing / Stopping) Processes – `kill`
  - To control a process, Linux uses signals.
    | Signal  | Meaning                     |
    | ------- | --------------------------- |
    | SIGTERM | Ask process to stop cleanly |
    | SIGKILL | Force kill (no cleanup)     |
    | SIGSTOP | Pause the process           |
    
  - Example: `kill 1337`

4. How Processes Start – `systemd`
  - When Linux boots:
    - First major process starts
    - That process is `systemd`
    - `systemd` has PID 1
    - All other processes are children of `systemd`
  
5. Starting Services on Boot – `systemctl`
   - `systemctl` talks to `systemd`
   - Syntax: `systemctl [option] [service]`
   - Common options:
       - `start` → start service now
       - `stop` → stop service
       - `enable` → start at boot
       - `disable` → don’t start at boot
   - Example: `systemctl start apache2`
6. Foreground vs Background Processes

In Linux, processes can operate in two main states: foreground and background. When a process runs in the foreground, it occupies the terminal and interacts directly with the user, meaning you can see its output and provide input to it. To start a foreground process, you simply execute it from the command line. On the other hand, background processes run independently of the terminal session, allowing you to continue using the terminal for other tasks. To send a process to the background,you can append an ampersand (&) at the end of the command.For example,`command &`.

> In Linux, using Ctrl + Z allows you to suspend a currently running foreground process, effectively putting it into the background. When you press Ctrl + Z, the operating system pauses the process and sends it to the background, where it remains in a stopped state. This is useful for temporarily halting processes without terminating them, allowing you to resume later. You can manage this suspended process using the `bg` command to continue its execution in the background or `fg` to bring it back to the foreground.

## What is cron?
- cron is a Linux service that: runs commands automatically at fixed times.
- Examples:
    - backup files every day
    - run a script every 12 hours
    - clean logs every week
## What is crontab?
- A crontab is just a schedule file for cron.
- You edit it using: `crontab -e`
- Cron job format:-
    - `MIN  HOUR  DOM  MON  DOW  COMMAND `
    - | Field | Meaning            |
      | ----- | ------------------ |
      | MIN   | Minute             |
      | HOUR  | Hour               |
      | DOM   | Day of month       |
      | MON   | Month              |
      | DOW   | Day of week        |
      | CMD   | Command to execute |
    > WHEN to run + WHAT to run
    - Example:- `0 */12 * * * cp -R /home/cmnatc/Documents /var/backups/`
    - | Field | Value | Meaning         |
      | ----- | ----- | --------------- |
      | MIN   | 0     | At minute 0     |
      | HOUR  | */12  | Every 12 hours  |
      | DOM   | *     | Any day         |
      | MON   | *     | Any month       |
      | DOW   | *     | Any day of week |

## What is a repository
A repository is a server that stores software packages in an organized way.

## What is APT?
we use the `apt` command to install software onto our Ubuntu system.`apt` contains a whole suite of tools that allows us to manage the packages and sources of our software, and to install or remove software at the same time
