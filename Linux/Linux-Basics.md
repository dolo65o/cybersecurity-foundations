## Where is Linux Used?

Linux is a command line operating system based on unix. There are multiple operating systems that are based on Linux.
Linux powers things such as:
- Websites that you visit
- Car entertainment/control panels
- Point of Sale (PoS) systems such as checkout tills and registers in shops
- Critical infrastructures such as traffic light controllers or industrial sensors

## Basic Linux Commands

| Command | Purpose | Example |
|------|--------|--------|
| `echo` | Display text on the terminal | `echo "Hello Friend!"` |
| `whoami` | Show the currently logged-in user | `whoami` |
| `ls` | List files and directories | `ls` |
| `cd` | Change directory | `cd Documents` |
| `cat` | Display contents of a file | `cat todo.txt` |
| `pwd` | Show current working directory | `pwd` |
| `find` | Search for files in directories | `find -name "passwords.txt"` |
| `grep` | Search text inside files | `grep "password" config.txt` |

## Shell Operators

| Symbol | Simple Meaning | Example |
|------|---------------|--------|
| `&` | Run command in background (terminal stays free) | `sleep 60 &` |
| `&&` | Run next command only if first works | `mkdir test && cd test` |
| `>` | Send output to file (old content is deleted) | `echo "Hello" > file.txt` |
| `>>` | Send output to file (old content is kept) | `echo "World" >> file.txt` |

