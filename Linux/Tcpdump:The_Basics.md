## tcpdump Essentials

`tcpdump` is a powerful command-line packet analyzer. Running it without arguments is rarely useful; you usually need to specify the interface and formatting.

**1. Network Interfaces**
   - Identify your active interface using `ip a`.
   - Capture on specific interface: `tcpdump -i ens5`
   - Capture on all interfaces: `tcpdump -i any`
    
**2. Managing Data**
   - Save to file: `tcpdump -w capture.pcap` (packets won't show in terminal).
   - Read from file: `tcpdump -r capture.pcap`
   - Limit count: `tcpdump -c 10` (stops after 10 packets).

**3. Formatting & Performance**
Use these flags to make the output readable and fast:
  - `-n`: Disable DNS resolution (show IP addresses).
  - `-nn`: Disable both DNS and port resolution (e.g., show 80 instead of http).
  - `-v`, `-vv`, `-vvv`: Increase verbosity for more packet detail.

### Quick Reference Table
| Flag | Function |
| :--- | :--- |
| `-i` | Select interface |
| `-w` | Write to file |
| `-r` | Read from file |
| `-c` | Packet limit |
| `-nn` | No name/port resolution |
| `-v` | Verbose output |

### Combined Example 
`sudo tcpdump -i ens5 -c 10 -nn -vv`

---

## Filtering 

In busy networks, thousands of packets flow every second. Filters help you isolate exactly what you need.

**A. Filtering by Host (IP/Domain)**
* **Specific Host:** `tcpdump host example.com` (captures traffic to/from the host).
* **Source Only:** `tcpdump src host 192.168.1.10` (traffic *from* this IP).
* **Destination Only:** `tcpdump dst host 192.168.1.10` (traffic *to* this IP).

**B. Filtering by Port**
Every service has a port (HTTP: 80, DNS: 53, SSH: 22).
* **Specific Port:** `tcpdump port 53` (captures all DNS traffic).
* **Source Port:** `tcpdump src port 443` (traffic sent *from* an HTTPS server).

**C. Filtering by Protocol**
You can filter by the protocol name directly:
* `tcpdump tcp`
* `tcpdump udp`
* `tcpdump icmp` (useful for troubleshooting `ping` requests).

**D. Logical Operators (and / or / not)**
Combine filters to get highly specific results:
* **AND:** `tcpdump host 1.1.1.1 and tcp` (TCP traffic involving that IP).
* **OR:** `tcpdump udp or icmp` (Captures either UDP or ICMP traffic).
* **NOT:** `tcpdump not port 22` (Shows everything *except* SSH traffic).

### Filtering While Reading 
You don't have to filter during the live capture; you can filter a saved `.pcap` file.

* **Apply filter to file:** `tcpdump -r traffic.pcap src host 192.168.1.1`
* **Count matching packets:** `tcpdump -r traffic.pcap port 80 | wc -l`

### Combined Example 
`sudo tcpdump -i any -nn tcp port 443 and host 10.0.0.5`

> *Meaning: Listen on all interfaces, don't resolve names, look for HTTPS traffic involving a specific internal IP.*

---

## Advanced Filtering: Length & Headers 

When host and port filters aren't enough, you can look inside the packet structure itself.

**A. Packet Length Filtering**
Useful for finding abnormally large or small packets (e.g., MTU issues).
* **Greater than:** `tcpdump greater 1000` (packets ≥ 1000 bytes).
* **Less than:** `tcpdump less 64` (packets ≤ 64 bytes).

**B. TCP Flag Filtering (The "Deep Dive")**
TCP uses flags to manage connections. These are stored as bits in the header.

* **Only SYN packets:** `tcpdump "tcp[tcpflags] == tcp-syn"` (initial connection requests).
* **Any packet with SYN set:** `tcpdump "tcp[tcpflags] & tcp-syn != 0"`
* **SYN or ACK packets:** `tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"`

**C. Custom Offset Filtering**
You can inspect specific bytes in a header using the syntax: `proto[offset:size]`.
* **Example:** `ip[0] & 0xf != 5` (looks at the first byte of the IP header to find packets with options enabled).

### Bitwise Operators Cheat Sheet 

Since packet headers are binary, `tcpdump` uses bitwise logic:

| Operator | Name | Logic |
| :--- | :--- | :--- |
| `&` | **AND** | Returns 1 only if both bits are 1. |
| `\|` | **OR** | Returns 1 if at least one bit is 1. |
| `!` | **NOT** | Reverses the bit (0 becomes 1). |

---
## Output Formatting Options 

Control how the data looks in your terminal to make it easier to read.

| Flag | Description | Use Case |
| :--- | :--- | :--- |
| `-q` | **Quick** | Minimal info; useful for high-speed viewing. |
| `-e` | **Ethernet** | Includes **MAC addresses** in the output. |
| `-A` | **ASCII** | Prints content as text (good for HTTP/unencrypted data). |
| `-xx` | **Hex** | Displays the raw packet|
| `-X` |**Hex and ASCII**| Displays both together|
