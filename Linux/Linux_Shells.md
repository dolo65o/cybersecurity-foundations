## What is Shell?

A Shell is the program that understands and execute your command

## Types of Linux Shells

Like the Command Prompt and PowerShell in Windows OS, Linux has different types of shells available, each with its own features and characteristics.
- Multiple shells are installed in different Linux distributions. To see which shell you are using, type: `echo $SHELL`
- list down the available shells in your Linux OS. The file `/etc/shells` contains all the installed shells on a Linux system. You can list down the available shells in your Linux OS by typing `cat /etc/shells` in the terminal.
- To switch between these shells, you can type the shell name that is present on your OS.
- To permanently change your default shell, you can use the command: `chsh -s /usr/bin/zsh` -> `zsh` is a shell name.

**There are many types of Linux shells.**
1. Bourne Again Shell
    * Bourne Again Shell (Bash) is the default shell for most Linux distributions.
    * It offers a tab completion feature.
    * Bash keeps a history file and logs all of your commands.
2. Friendly Interactive Shell
    * It offers a very simple syntax, which is feasible for beginner users.
    * Unlike bash, it has auto spell correction for the commands you write.
    * You can customize the command prompt with some cool themes using fish.
3. Z Shell
    * Zsh provides advanced tab completion and is also capable of writing scripts.
    * Just like fish, it also provides auto spell correction for the commands.
    * It offers extensive customization that may make it slower than other shells.
---

## Shell Scripting and Components
A shell script is nothing but a set of commands. Suppose a repetitive task requires you to enter multiple commands using a shell. Instead of entering them one after one on every repetition of that task, which may take more of your time, you can combine them into a script. To execute all those commands, you will only execute the script, and all the commands will be executed.
- Scripting can be done in various programming languages as well.
- We first need to create a file using any text editor for the script. The file must be named with an extension `.sh`, the default extension for bash scripts.
    * Ex:- `nano first_script.sh`
> Every script should start from shebang. Shebang is a combination of some characters that are added at the beginning of a script, starting with `#!` followed by the name of the interpreter to use while executing the script. As we are writing our script in bash, let’s define it as the interpreter in the shebang: `#!/bin/bash`

### Variables
- A variable stores a value inside it.
- Example:-
```
# Defining the Interpreter 
#!/bin/bash
echo "Hey, what’s your name?"
read name
echo "Welcome, $name"
```
    - Line 1 Comment
    - Line 2 Shebang
    - Line 3 Printing message
    - Line 4 Asking for input which is saved in variable(name)
    - printing message with vairable value
- Now, save the script by pressing `CTRL+X`. Confirm by pressing `Y` and then `ENTER`.
- To execute the script, we first need to make sure that the script has execution permissions. To give these permissions to the script, we can type:- `chmod +x first_script.sh`
- Now that the script has execution permissions use `./` before the script name to execute it.

### Loops
- Loop, as the name suggests, is something that is repeating.
- Example:- loop that will display all numbers starting from 1 to 10 on the screen.
```
# Defining the Interpreter 
#!/bin/bash
for i in {1..10};
do
echo $i
done
```
> first line has the variable i that will iterate from 1 to 10 and execute the below code every time. do indicates the start of the loop code, and done indicates the end.

### Conditional Statements
- Help you execute a specific code only when a condition is satisfied.
- Example:-  You will create a conditional statement that will first ask the user their name, and if that name matches the high authority user’s name, it will display the secret.
```
# Defining the Interpreter 
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Stewart" ]; then
        echo "Welcome Stewart! Here is the secret: THM_Script"
else
        echo "Sorry! You are not authorized to access the secret."
fi
```
> The above script takes the user’s name as input and stores it into a variable (studied in the Variables section). The conditional statement starts with if and compares the value of that variable with the string Stewart; if it’s a match, it will display the secret to the user, or else it will not. The fi is used to end the condition.

---
**Example of Shell Script **

*The Locker Script*
- A user has a locker in a bank. To secure the locker, we have to have a script in place that verifies the user before opening it. When executed, the script should ask the user for their name, company name, and PIN. If the user enters the following details, they should be allowed to enter, or else they should be denied access.

- Username: John
- Company name: Tryhackme
- PIN: 7385

***Script***
```
# Defining the Interpreter 
#!/bin/bash 

# Defining the variables
username=""
companyname=""
pin=""

# Defining the loop
for i in {1..3}; do
# Defining the conditional statements
        if [ "$i" -eq 1 ]; then
                echo "Enter your Username:"
                read username
        elif [ "$i" -eq 2 ]; then
                echo "Enter your Company name:"
                read companyname
        else
                echo "Enter your PIN:"
                read pin
        fi
done

# Checking if the user entered the correct details
if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
        echo "Authentication Successful. You can now access your locker, John."
else
        echo "Authentication Denied!!"
fi
```
***Script Execution***

```
user@tryhackme:~$ ./locker_script.sh
Enter your Username:
John
Enter your Company name:
Tryhackme
Enter your PIN:
1349
Authentication Denied!!

```
---
