Metasploit is an open-source penetration testing framework that helps security professionals find and exploit vulnerabilities in computer systems. It includes a database of known vulnerabilities and tools and scripts for exploiting them.
- The Metasploit Framework is a set of tools that allow information gathering, scanning, exploitation, exploit development, post-exploitation, and more.
- The main components of the Metasploit Framework:
    - msfconsole: The main command-line interface.
    - Modules: small tools inside Metasploit designed to perform specific tasks
    - Tools: Stand-alone tools that will help vulnerability research, vulnerability assessment, or penetration testing. Some of these tools are msfvenom, pattern_create and pattern_offset.
---
## Main Components
While using the Metasploit Framework, you will primarily interact with the Metasploit console.Using the `msfconsole` command
* Few recurring concepts: vulnerability, exploit, and payload.
  - **Exploit**: A piece of code that uses a vulnerability present on the target system.
  - **Vulnerability**: A vulnerability is a weakness in a system’s design, implementation, or configuration.
  - **Payload**: A payload is the code that runs on the target system after successful exploitation.
  - **Modules**: small tools inside Metasploit designed to perform specific tasks.

## Types of Modules in Metasploit
### Auxiliary Modules 
Used for scanning and information gathering.Do NOT usually give shell access.Any supporting module, such as scanners, crawlers and fuzzers, can be found here.
```bash
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 auxiliary/
auxiliary/
├── admin
├── analyze
├── bnat
├── client
├── cloud
├── crawler
├── docx
├── dos
├── example.py
├── example.rb
├── fileformat
├── fuzzers
├── gather
├── parser
├── pdf
├── scanner
├── server
├── sniffer
├── spoof
├── sqli
├── voip
└── vsploit

20 directories, 2 files
```

---
### Encoders

Encoders are used to **modify (encode) exploits and payloads** so they are harder for antivirus or security systems to detect.They change the appearance of the payload **without changing its function**.

Many antivirus systems use **signature-based detection**.

Signature-based detection works by:

1. Storing patterns of known malware
2. Comparing files against these patterns
3. Raising an alert if a match is found

If a payload matches a known signature → antivirus blocks it.

Encoders help avoid this detection by changing the payload's structure.


> Modern antivirus may still detect encoded payloads using:- Behaviour analysis, Heuristic detection, Machine learning detection

> Therefore, encoders have **limited success rate**.

#### Common Encoder Categories

```bash
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 encoders/
encoders/
├── cmd
├── generic
├── mipsbe
├── mipsle
├── php
├── ppc
├── ruby
├── sparc
├── x64
└── x86

10 directories, 0 files
```

| Folder | Description |
|--------|-------------|
| cmd | command encoders |
| generic | general purpose encoders |
| php | php payload encoding |
| ruby | ruby payload encoding |
| x86 | encoder for 32-bit architecture |
| x64 | encoder for 64-bit architecture |
| mipsbe | MIPS big-endian encoding |
| mipsle | MIPS little-endian encoding |
| ppc | PowerPC encoding |
| sparc | SPARC architecture encoding |

---
### Evasion

Evasion modules are used to help payloads **bypass antivirus and security detection mechanisms**.

They are specifically designed to avoid detection from:

- Antivirus software
- Windows Defender
- Security monitoring tools

#### Difference Between Encoder and Evasion

Encoders:
- Modify payload structure
- Mainly try to bypass signature-based detection
- Limited effectiveness

Evasion modules:
- Use advanced techniques to avoid detection
- Attempt to bypass security protections directly
- More practical than encoders


#### Example Evasion Modules (Windows)

```bash
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 2 evasion/
evasion/
└── windows
    ├── applocker_evasion_install_util.rb
    ├── applocker_evasion_msbuild.rb
    ├── applocker_evasion_presentationhost.rb
    ├── applocker_evasion_regasm_regsvcs.rb
    ├── applocker_evasion_workflow_compiler.rb
    ├── process_herpaderping.rb
    ├── syscall_inject.rb
    ├── windows_defender_exe.rb
    └── windows_defender_js_hta.rb

1 directory, 9 files
```

| Module | Purpose |
|--------|--------|
| applocker_evasion_install_util.rb | bypass Windows AppLocker restrictions |
| applocker_evasion_msbuild.rb | bypass AppLocker using MSBuild |
| applocker_evasion_presentationhost.rb | bypass using PresentationHost |
| applocker_evasion_regasm_regsvcs.rb | bypass via .NET tools |
| applocker_evasion_workflow_compiler.rb | bypass using workflow compiler |
| process_herpaderping.rb | disguises malicious process behavior |
| syscall_inject.rb | injects payload using system calls |
| windows_defender_exe.rb | attempts to evade Windows Defender |
| windows_defender_js_hta.rb | bypass using HTA execution |

---
### Exploit

Exploit modules are used to **take advantage of vulnerabilities** in a target system.

An exploit is a piece of code that uses a weakness (vulnerability) to gain unauthorized access or execute commands on the target.

> Metasploit organizes exploits based on operating system or software platform.

#### Example categories:
```bash
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 exploits/
exploits/
├── aix
├── android
├── apple_ios
├── bsd
├── bsdi
├── dialup
├── example_linux_priv_esc.rb
├── example.py
├── example.rb
├── example_webapp.rb
├── firefox
├── freebsd
├── hpux
├── irix
├── linux
├── mainframe
├── multi
├── netware
├── openbsd
├── osx
├── qnx
├── solaris
├── unix
└── windows

20 directories, 4 files
```

| Directory | Target System |
|----------|--------------|
| windows | Windows OS vulnerabilities |
| linux | Linux OS vulnerabilities |
| unix | Unix-based systems |
| android | Android OS |
| apple_ios | iOS devices |
| osx | macOS |
| freebsd | FreeBSD systems |
| openbsd | OpenBSD systems |
| solaris | Solaris OS |
| aix | IBM AIX systems |
| hpux | HP-UX systems |
| firefox | Firefox browser vulnerabilities |
| multi | multi-platform exploits |
| mainframe | mainframe systems |

---

### NOP 

NOP stands for **No Operation**.

NOP instructions literally **do nothing** when executed by the CPU.

Example (Intel x86):

0x90 → instruction that tells CPU to do nothing for one cycle.

NOPs are used to:

- Adjust payload size
- Improve exploit reliability
- Create buffer space before payload execution
- Ensure the payload executes correctly

NOPs act as a **placeholder or padding** inside the exploit code.

> A sequence of multiple NOP instructions is called: **NOP sled**

> Example: `NOP NOP NOP NOP PAYLOAD`

> Even if the exact memory location is not perfect, execution will slide through NOPs until reaching the payload.


#### NOP Categories by Architecture

```bash
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 nops/
nops/
├── aarch64
├── armle
├── cmd
├── mipsbe
├── php
├── ppc
├── sparc
├── tty
├── x64
└── x86

10 directories, 0 files
```

| Folder | Architecture |
|--------|--------------|
| x86 | 32-bit systems |
| x64 | 64-bit systems |
| armle | ARM architecture |
| aarch64 | 64-bit ARM |
| mipsbe | MIPS big-endian |
| ppc | PowerPC |
| sparc | SPARC |
| php | PHP environments |
| cmd | command payloads |
| tty | terminal related |

---
### Payload

A payload is the code that runs on the target system **after a successful exploit**.

Exploit → creates entry  
Payload → performs action

Payloads allow attackers to:

- Execute commands
- Open shell access
- Install backdoor
- Run programs (example: calc.exe)
- Control the target system

---



#### Payload Structure

There are four main types of payload directories:
```bash
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 payloads/
payloads/
├── adapters
├── singles
├── stagers
└── stages

4 directories, 0 files
```

- **adapters**: wrapping single payloads and converting them into different formats.An adapter can take a basic payload and modify it to fit different platforms or communication protocols,
- **singles**: Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run
- **stagers**: establishing connection between attacker and victim.Preparing environment for full payload
- **stages**: Stages contain the full payload functionality.They are downloaded after the stager connects successfully.


#### Difference Between Single and Staged Payload

Single payload:`shell_reverse_tcp`

Staged payload:`shell/reverse_tcp`

Difference:

"_" indicates single payload  
"/" indicates staged payload
---

### Post 

Post modules are used **after a successful exploitation**.They help attackers perform actions on a system where access has already been obtained.

> This phase is called:post-exploitation


#### Purpose of Post Modules

Post modules allow attackers to:

- Gather system information
- Extract saved passwords
- Capture screenshots
- Collect network details
- Escalate privileges
- Maintain persistence
- Move laterally to other systems

> Post modules are used **after getting access to the target system**.
> Metasploit organizes post modules based on operating system or environment.

#### Example directories:

```bash
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 post/
post/
├── aix
├── android
├── apple_ios
├── bsd
├── firefox
├── hardware
├── linux
├── multi
├── networking
├── osx
├── solaris
└── windows

12 directories, 0 files
```
| Directory | Target |
|----------|--------|
| windows | Windows systems |
| linux | Linux systems |
| android | Android devices |
| apple_ios | iOS devices |
| osx | macOS systems |
| multi | multi-platform modules |
| networking | network information gathering |
| hardware | hardware-related tasks |
| firefox | browser-related modules |
| solaris | Solaris OS |
| aix | IBM AIX systems |
| bsd | BSD systems |

---

