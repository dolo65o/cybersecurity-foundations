# Nmap Essentials: Host Discovery & Port Scanning

Nmap (Network Mapper) is the industry-standard tool for network discovery. It allows you to find live hosts and identify the services running on them.

---

## 1. Host Discovery: "Who is Online?" 

Before scanning ports, you must find live devices. Nmap provides several ways to specify and find targets.

### Specifying Targets 
* **IP Range:** `192.168.0.1-10` (scans IPs .1 through .10).
* **Subnet:** `192.168.0.1/24` (scans all 256 addresses in the subnet).
* **Hostname:** `example.thm`.

### Discovery Methods
* **Ping Scan (`-sn`):** Discovers live hosts without scanning ports. It is fast and less "noisy".
* **List Scan (`-sL`):** Simply lists the targets that *would* be scanned without sending any packets to them.
* **Local vs. Remote:**
    * **Local:** Uses ARP requests if you are on the same Ethernet/WiFi network.
    * **Remote:** Uses ICMP Echo (ping), TCP SYN to port 443, and TCP ACK to port 80 to see if a host responds.

---

## 2. TCP Port Scanning 

A service is a process listening on a TCP or UDP port (e.g., Web on 80/443, DNS on 53).

### A. TCP Connect Scan (`-sT`) 
The most basic scan that completes the full **TCP three-way handshake**.
* **Open Port:** `SYN` → `SYN-ACK` → `ACK`. Once established, Nmap sends `RST-ACK` to tear it down.
* **Closed Port:** The target responds with a `RST-ACK` packet.
* **Pro/Con:** Very accurate but leaves clear traces in application logs.


### B. SYN Scan (`-sS`) — Stealth Mode 
Known as a "half-open" scan because it never completes the handshake.
* **Open Port:** Target sends `SYN-ACK`. Nmap immediately responds with `RST` to kill the connection.
* **Closed Port:** Same as connect scan (`RST-ACK`).
* **Advantage:** Stealthier as it often bypasses application-level logging.

---

## 3. UDP Port Scanning (`-sU`) 

UDP is connectionless, making it slower and harder to scan than TCP.
* **Logic:** Nmap sends UDP packets and waits for a response.
* **Closed Port Indicator:** The target sends back an **ICMP Destination Unreachable (Port Unreachable)** message.
* **Use Case:** Crucial for finding DNS, DHCP, and VoIP services.

---

## 4. Port Selection & Optimization 

Nmap scans the top 1,000 common ports by default. Use these flags to be more specific:

| Option | Function |
| :--- | :--- |
| `-F` | **Fast mode**: Scans only the 100 most common ports. |
| `-p [range]` | Scan specific ports (e.g., `-p22-80` or `-p80,443`). |
| `-p-` | Scan **all** 65,535 ports (most thorough). |
| `-p1-1023` | Scans **well-known ports** (standard services). |

---

# Nmap Advanced: OS & Version Detection 

Once you know a port is open, the next step is to gather intelligence: *What exactly is running on that port?* and *What operating system is the target using?*

---

## 1. OS Detection (`-O`) 
Nmap analyzes network traffic behaviors (like TCP/IP stack fingerprints) to make an **educated guess** about the target's operating system.

* **Flag:** `nmap -O <target>`
* **How it works:** It looks at subtle differences in how operating systems implement network standards.
* **Accuracy:** It provides a probability score (e.g., "Linux 4.X | 5.X"). It is not always 100% accurate but gives a very close estimation.

## 2. Service Version Detection (`-sV`) 
Knowing a port is open (e.g., Port 22) isn't enough. You need to know the **specific software version** (e.g., OpenSSH 8.9p1) to find vulnerabilities.

* **Flag:** `nmap -sV <target>`
* **Benefit:** Instead of just saying `22/tcp open ssh`, it reports:
  > `22/tcp open ssh OpenSSH 8.9p1 Ubuntu 3ubuntu0.10`
* **Use Case:** Essential for identifying outdated or vulnerable services.

## 3. Aggressive Scan (`-A`) 
If you want "everything" in one go, use the aggressive scan option.

* **Flag:** `nmap -A <target>`
* **What it enables:**
    * OS Detection (`-O`)
    * Version Detection (`-sV`)
    * Traceroute
    * Script Scanning (Default scripts)
> **Warning:** This scan is very noisy and easily detected by firewalls/IDS.

## 4. Forcing the Scan (`-Pn`) 
Sometimes a target is online but blocks ping requests (ICMP), making Nmap think it is "down."

* **Flag:** `nmap -Pn <target>`
* **Function:** Tells Nmap to **skip host discovery** and treat **all** hosts as online.
* **Use Case:** useful against Windows hosts or firewalls that block ICMP (ping).

---

# Nmap Advanced: Timing & Performance Control 

Nmap scans can be adjusted for speed or stealth. Running a scan at full speed might trigger Intrusion Detection Systems (IDS) or crash a fragile target, while running too slowly can take hours. Nmap provides templates and granular controls to manage this.

---

## 1. Timing Templates (`-T<0-5>`) 
Nmap offers six predefined timing templates. You can select them by number (`-T4`) or name (`-T aggressive`).

| Template | Name | Use Case | Behavior |
| :--- | :--- | :--- | :--- |
| **`-T0`** | **Paranoid** | IDS Evasion | Extremely slow. Waits **5 minutes** between probes. |
| **`-T1`** | **Sneaky** | IDS Evasion | Slow. Waits **15 seconds** between probes. |
| **`-T2`** | **Polite** | Low Noise | Waits **0.4 seconds** between probes to reduce network load. |
| **`-T3`** | **Normal** | **Default** | Standard speed. Dynamic based on network responsiveness. |
| **`-T4`** | **Aggressive** | **Recommended** | Fast and reliable on modern networks. |
| **`-T5`** | **Insane** | Speed only | Very fast but likely to lose packets or crash targets. |

> **Real-world comparison:** Scanning 100 ports might take **9.8 hours** with `-T0` but only **0.13 seconds** with `-T4`.

## 2. Fine-Tuning Performance 
If the templates don't fit your specific needs, you can manually control the scan behavior.

### A. Parallelism (Probes at once)
Control how many probes Nmap sends simultaneously.
* **Flags:** `--min-parallelism <number>` and `--max-parallelism <number>`
* **Usage:** Increasing parallelism speeds up scans on stable networks but may cause packet drops on poor networks.

### B. Scan Rate (Packets per second)
Control the traffic rate directly.
* **Flags:** `--min-rate <number>` and `--max-rate <number>`
* **Usage:** Useful if you know exactly how much traffic the network can handle (e.g., forcing 100 packets/sec).

### C. Host Timeout
Prevent Nmap from getting stuck on a slow or unresponsive host.
* **Flag:** `--host-timeout <time>`
* **Usage:** Specifies the maximum time to wait for a target host before giving up and moving to the next one.

---

# Nmap Advanced: Verbosity & Saving Results

By default, Nmap only prints the final summary. However, during long scans, you often need real-time updates to know the scan is still running or to see open ports as they are found. Furthermore, saving your results is critical for documentation.

---

## 1. Verbosity & Debugging

Verbosity allows you to see what Nmap is doing "under the hood" while the scan is running.

### A. Verbose Output (`-v`)
Adds detail to the output, showing you step-by-step actions (e.g., "Initiating ARP Ping", "Discovered open port 80").
* **Flag:** `-v` (Standard verbosity)
* **More Detail:** `-vv` or `-v2` (Increased verbosity)
* **Live Update:** You can also press `v` on your keyboard *during* a scan to increase verbosity dynamically.

### B. Debugging Output (`-d`)
If verbosity isn't enough, debugging mode floods the terminal with low-level details (packet contents, internal logic).
* **Flag:** `-d` (Basic debugging)
* **Max Level:** `-d9` (Maximum debugging; produces thousands of lines).
* **Use Case:** Only use this if you suspect Nmap is malfunctioning or need to troubleshoot specific network errors.

---

## 2. Saving Scan Reports 

You should always save your scan results. Nmap provides three main formats.

### A. Normal Output (`-oN`)
Saves the output exactly as it appears in the terminal.
* **Command:** `nmap -oN scan-results.txt <target>`
* **Best for:** Human reading and basic reporting.

### B. XML Output (`-oX`)
Saves the output in XML format.
* **Command:** `nmap -oX scan-results.xml <target>`
* **Best for:** Importing results into other tools like Metasploit, Zenmap, or custom scripts.

### C. Grepable Output (`-oG`)
Saves the output with one host per line.
* **Command:** `nmap -oG scan-results.gnmap <target>`
* **Best for:** Using command-line tools like `grep`, `awk`, or `cut` to quickly extract lists of IP addresses with specific open ports.

### D. "All" Formats (`-oA`) — **Recommended** 
Saves all three formats simultaneously.
* **Command:** `nmap -oA my-scan <target>`
* **Result:** Creates three files:
    1. `my-scan.nmap` (Normal)
    2. `my-scan.xml` (XML)
    3. `my-scan.gnmap` (Grepable)

---
