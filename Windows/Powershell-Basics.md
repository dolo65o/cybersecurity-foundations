## 1. What is PowerShell?

PowerShell is a **command-line shell and scripting language** developed by Microsoft.

It is used for:
- Task automation
- System administration
- Configuration management

Unlike old CMD, PowerShell works with **objects**, not just text.

---

## 2. Why PowerShell Was Created

Old Windows tools:
- cmd
- batch files

Problems:
- Worked only with text
- Hard to automate
- Limited control

PowerShell was created to:
- Work with structured data (objects)
- Automate complex tasks
- Integrate with Windows and .NET

Later, PowerShell became:
- Cross-platform
- Works on Windows, Linux, macOS

---

## 3. PowerShell is Object-Oriented

In PowerShell:
- Everything is an **object**
- Objects have:
  - Properties (data)
  - Methods (actions)

> In programming, an object represents an item with properties (characteristics) and methods (actions). For example, a car object might have properties like Color, Model, and FuelLevel, and methods like Drive(), HonkHorn(), and Refuel().

---
## Basic Syntax: Verb-Noun
- `Get-Content`: Retrieves (gets) the content of a file and displays it in the console.
- `Set-Location`: Changes (sets) the current working directory.
- `Get-Command`: Show me everything PowerShell can do.
- `Get-Alias`: lists all aliases available.
  * For example, `dir` is an alias for `Get-ChildItem`, and `cd` is an alias for `Set-Location`.
  * 
- `Find-Module`: Search online for extra PowerShell features.
- `Install-Module`: Download and install new PowerShell commands.
- `Get-Help`: What the command does
  * Example:- To see the examples, type: `get-help Get-Date -examples`.
  * For more information, type: `get-help Get-Date -detailed`.
  * For technical information, type: `get-help Get-Date -full`.
  * For online help, type: `get-help Get-Date -online`.

> Filter commands- `Get-Command -CommandType function` :- Show me only function not everything.
---
## Navigating the File System and Working with Files
- Listing files - `Get-chilItem` :- Shows all files and folders in the current directory,same as `ls` in linux and `dir` in cmd prompt.
- Changing Directory – `Set-Location` :- It changes the current directory, bringing us to the specified path,just like `cd` command in linux.
- Creating Files & Folders – `New-Item` :- Example: `New-Item -Path ".\captain-cabin\captain-wardrobe" -ItemType "Directory"`
- Deleting Files or Folders – `Remove-Item` :- Example: `Remove-Item -Path ".\captain-cabin\captain-wardrobe\captain-boots.txt"`
- Copying Files – `Copy-Item` :- Example: `Copy-Item -Path .\captain-cabin\captain-hat.txt -Destination .\captain-cabin\captain-hat2.txt`

---
## What is Piping (|)?
Piping is a technique used in command-line environments that allows the output of one command to be used as the input for another. This creates a sequence of operations where the data flows from one command to the next. 
- Piping is even more powerful because it passes objects rather than just text. These objects carry not only the data but also the properties and methods that describe and interact with the data.
### Sorting Files by Size
`Get-ChildItem | Sort-Object Length` :- Lists all files | Sorts them by size (small → large)
### Filtering Files (Where-Object)
* `Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"`
  * `Get-ChildItem `→ get all files
  * `Where-Object` → filter them
  * `-Property` "Extension" → check file extension
  * `-eq `".txt" → only .txt files

#### Comparison Operators
| Operator | Meaning               |
| -------- | --------------------- |
| `-eq`    | equal                 |
| `-ne`    | not equal             |
| `-gt`    | greater than          |
| `-ge`    | greater than or equal |
| `-lt`    | less than             |
| `-le`    | less than or equal    |
| `-like`  | pattern matching      |

### Filtering by Name
- Example:- `Get-ChildItem | Where-Object -Property Name -like "ship*"`
- Only files whose names start with ship are shown.

### Combining Commands (Pipeline Power)
- `Get-ChildItem |Sort-Object Length -Descending |Select-Object -First 1`
  - Gets all files
  - Sorts them by size (largest first)
  - Shows only the biggest file

### Searching Inside Files (Select-String)
- `Select-String -Path ".\captain-hat.txt" -Pattern "hat"`
    - Open the file
    - Search for the word "hat"
    - Show the line where it appears
---
## System and Network Information
- `Get-ComputerInfo` :- cmdlet retrieves comprehensive system information, including operating system information, hardware specifications, BIOS details, and more.
- `Get-LocalUser` :- lists all the local user accounts on the system.
- `Get-NetIPConfiguration` :- provides detailed information about the network interfaces on the system, including IP addresses, DNS servers, and gateway configurations.
- `Get-NetIPAddress` :- cmdlet will show details for all IP addresses configured on the system.

---
## Real-Time System Analysis
- `Get-Process` :- provides a detailed view of all currently running processes, including CPU and memory usage.
- `Get-Service` :- allows the retrieval of information about the status of services on the machine, such as which services are running, stopped, or paused.
- `Get-NetTCPConnection` :- displays current TCP connections, giving insights into both local and remote endpoints.
- `Get-FileHash` :- as a useful cmdlet for generating file hashes, which is particularly valuable in incident response, threat hunting, and malware analysis, as it helps verify file integrity and detect potential tampering.

---
## Scripting
- Scripting is the process of writing and executing a series of commands contained in a text file, known as a script, to automate tasks that one would generally perform manually in a shell, like PowerShell.
- Scripting is like giving a computer a to-do list, where each line in the script is a task that the computer will carry out automatically. This saves time, reduces the chance of errors, and allows to perform tasks that are too complex or tedious to do manually.
- `Invoke-Command` cmdlet :- is essential for executing commands on remote systems.
- Example :- `Invoke-Command -ComputerName PC1 -ScriptBlock { Get-Process }`
  * Connect to computer PC1
  * Run `Get-Process`
  * Return the result to your system
