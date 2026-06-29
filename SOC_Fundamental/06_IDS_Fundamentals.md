## IDS — Intrusion Detection System

### What is IDS?
Monitors network traffic **inside** the network and detects malicious activity that already passed the firewall.

> Analogy: Firewall = building gatekeeper. IDS = surveillance cameras inside the building.

### Key Points
- Sits inside the network, not at the boundary
- Detects threats using **signature-based** and **anomaly-based** detection
- **Does NOT block traffic** — only generates alerts for security administrators
- Catches attackers who bypassed the firewall via legitimate-looking connections

### Firewall vs IDS

| | Firewall | IDS |
|-|----------|-----|
| **Position** | Network boundary | Inside the network |
| **Function** | Allow/block traffic before connection | Monitor traffic after it enters |
| **Action** | Blocks traffic | Alerts only — no blocking |
| **Analogy** | Gatekeeper | Surveillance camera |

## IDS — Deployment & Detection Modes

### Deployment Modes

| Type | Scope | Pros | Cons |
|------|-------|------|------|
| **HIDS** (Host-based) | Single host | Detailed host visibility | Resource-intensive; hard to manage at scale |
| **NIDS** (Network-based) | Entire network | Centralized view of all network detections | Less visibility into individual host activity |

---

### Detection Modes

| Type | How it works | Detects Zero-day? | Weakness |
|------|-------------|-------------------|----------|
| **Signature-based** | Matches traffic against known attack signatures in DB | No | Can't detect unknown/new attacks |
| **Anomaly-based** | Learns baseline behavior; alerts on deviations | Yes | High false positive rate |
| **Hybrid** | Combines both methods | Yes | Complexity |

**Zero-day attacks** = attacks with no prior known signature — only anomaly-based or hybrid IDS can catch these.

**Reducing false positives** in anomaly-based IDS → fine-tune by manually defining normal baseline behavior.

---

### Choosing the Right IDS

| Scenario | Best Fit |
|----------|---------|
| Small, known threat surface | Signature-based |
| Modern/zero-day threats | Anomaly-based or Hybrid |
| Best of both worlds | Hybrid |

---

## Snort — Open-Source IDS

### What is Snort?
- Open-source IDS developed in **1998**
- Uses **signature-based + anomaly-based** detection
- Rules defined in rule files (built-in + custom)
- Custom rules can be created; built-in rules can be disabled

---

### Snort Modes

| Mode | What it does | Use Case |
|------|-------------|---------|
| **Packet Sniffer** | Reads and displays packets — no analysis; output to console or file | Network troubleshooting/diagnostics |
| **Packet Logging** | Logs all network traffic to **PCAP** file for later analysis | Forensic investigation / root cause analysis |
| **NIDS Mode** | Monitors traffic in real-time; applies rule files; generates alerts on matches | Primary IDS function — proactive threat detection |

---

### Rules in Snort
- **Built-in rules** — pre-installed; cover wide range of known attack patterns
- **Custom rules** — created by analysts for specific detection needs
- Built-in rules can be **disabled** if not relevant to your environment

> PCAP files from packet logging mode can be used by forensic investigators to reconstruct past attacks

---

## Snort — Rules & Usage

### Key Directories & Files
```
/etc/snort/
├── snort.lua          # Main config (network range, enabled rules, settings)
├── snort.conf
├── rules/
│   └── local.rules    # Custom rules go here
├── threshold.conf
└── Intro_to_IDS.pcap
```

---

### Rule Format
```
action protocol src_ip src_port -> dst_ip dst_port (msg:"..."; sid:XXXXX; rev:X;)
```

**Example — detect ICMP ping to loopback:**
```
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
```

### Rule Components

| Field | Example | Description |
|-------|---------|-------------|
| **Action** | `alert` | What to do when rule matches |
| **Protocol** | `icmp` | Traffic protocol to match |
| **Source IP** | `any` | Origin IP (`any` = all) |
| **Source Port** | `any` | Origin port |
| **Direction** | `->` | Traffic flow direction |
| **Destination IP** | `$HOME_NET` | Target IP (variable from config) |
| **Destination Port** | `any` | Target port |
| **msg** | `"Ping Detected"` | Alert message displayed on trigger |
| **sid** | `10001` | Unique rule identifier |
| **rev** | `1` | Revision number — increment on each edit |

---

### Adding a Custom Rule
```bash
sudo nano /etc/snort/rules/local.rules
# Add rule, then Ctrl+X → Y to save
```

---

### Running Snort

**Real-time detection on network interface:**
```bash
sudo snort -q -l /var/log/snort -i lo -A alert_fast -c /etc/snort/snort.lua
```

**Run on PCAP file (forensic/historical analysis):**
```bash
sudo snort -q -l /var/log/snort -r Task.pcap -A alert_fast -c /etc/snort/snort.lua
```

| Flag | Purpose |
|------|---------|
| `-q` | Quiet mode — suppress banner |
| `-l` | Log output directory |
| `-i` | Network interface to monitor |
| `-r` | Read from PCAP file |
| `-A alert_fast` | Fast alert output format |
| `-c` | Path to config file |

---

### Sample Alert Output
```
07/24-10:46:52 [**] [1:1000001:1] "Loopback Ping Detected" [**] {ICMP} 127.0.0.1 -> 127.0.0.1
```
