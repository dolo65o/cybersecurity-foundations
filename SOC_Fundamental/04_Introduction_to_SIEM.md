## Log Sources & SIEM Need

### Host-Centric Log Sources
Logs from activity **on** the device (Windows, Linux, servers)

- File access by a user
- Authentication attempts
- Process execution
- Registry key add/edit/delete
- PowerShell execution

### Network-Centric Log Sources
Logs from activity **between** devices (firewalls, IDS/IPS, routers)

- SSH connections
- FTP file access
- Web traffic
- VPN access
- Network file sharing

---

### Why Manual Log Analysis Fails

| Problem | Why it hurts |
|---------|-------------|
| **Numerous sources** | Hundreds of events/second across many devices |
| **No centralization** | Must SSH/RDP into each device individually — extremely slow |
| **Limited context** | A single log looks harmless; only correlation reveals the full attack story |
| **Limited analysis** | Humans can't manually process thousands of logs/sec — critical events get missed |
| **Format issues** | Every log source uses a different format — hard to parse across multiple sources |

> **Example of limited context:** A file access event looks normal alone. Correlated with other logs, it reveals the user reached that machine via lateral movement after compromising another host.

---

## SIEM — Security Information and Event Management

> Solves all log management challenges by centralizing, normalizing, correlating, and alerting on log data.

---

### Core Features

#### 1. Centralized Log Collection
- Pulls logs from all sources (endpoints, servers, firewalls, etc.) via **agents or APIs**
- Single location for all logs — no more SSH-ing into individual machines

#### 2. Normalization
- **Parsing** — breaking a raw log into individual fields
- **Normalization** — converting all log formats into one consistent format
- Allows uniform analysis across Windows, Linux, firewalls, etc.

#### 3. Correlation
Finds relationships between logs across different sources to identify attack patterns.

**Example — 5 events in 5 minutes (all look innocent alone):**
```
1. Haris logs in via VPN from a never-before-seen IP
2. Haris accesses documents on a shared drive
3. Haris executes a PowerShell script
4. System makes an outbound network connection
```
→ Correlated = likely **data exfiltration** via compromised VPN credentials

#### 4. Real-time Alerting
- Built-in default detection rules + custom analyst-created rules
- Alert fires when rule conditions are met → analyst is notified
- Analyst investigates directly within the SIEM platform

#### 5. Dashboards & Reporting
Normalized data presented as actionable insights. Includes:
- Alert highlights
- Failed login attempts
- Events ingested count
- Rules triggered
- Top domains visited
- System/health notifications

---

## SIEM — Log Sources & Ingestion Methods

### Common Log Sources

#### Windows
- Logs viewed via **Event Viewer**; each event has a unique ID
- Windows endpoint logs forwarded to SIEM via agent

#### Linux — Key Log Locations

| Path | Contains |
|------|---------|
| `/var/log/httpd` | HTTP request/response and error logs |
| `/var/log/cron` | Cron job events |
| `/var/log/auth.log` / `/var/log/secure` | Authentication logs |
| `/var/log/kern` | Kernel events |

**Sample cron log:**
```
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-daily)
Jun 13 07:46:22 ebr crond[3592]: unable to exec /usr/sbin/sendmail: cron output for user root job sys-daily to /dev/null
```

#### Web Server (Apache)
Log locations: `/var/log/apache` or `/var/log/httpd`

**Sample Apache log:**
```
192.168.21.200 - - [21/March/2022:10:17:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395 "-" "Mozilla/5.0..."
127.0.0.1 - - [21/March/2022:10:22:04 -0300] "GET / HTTP/1.0" 200 2216 "-" "curl/7.68.0"
```

---

### Log Ingestion Methods

| Method | How it works |
|--------|-------------|
| **Agent / Forwarder** | Lightweight tool installed on endpoint; captures and ships logs to SIEM (Splunk calls it "Forwarder") |
| **Syslog** | Widely used protocol; collects from web servers, DBs, etc. and sends real-time to SIEM |
| **Manual Upload** | Offline log files uploaded directly for quick analysis (supported by Splunk, ELK, etc.) |
| **Port Forwarding** | SIEM listens on a specific port; endpoints push logs to that port |

---

## SIEM — Detection Rules & Alert Investigation

### How Detection Rules Work
Logical expressions that trigger alerts when specific conditions are met in log data.

**Examples:**
- 5 failed logins in 10 seconds → alert `Multiple Failed Login Attempts`
- Successful login after multiple failures → alert `Successful Login After Multiple Failed Attempts`
- USB plugged in (if restricted by policy) → alert
- Outbound traffic > 25MB → alert `Potential Data Exfiltration`

---

### Rule Creation — Use Cases

**Use Case 1 — Event Log Cleared**
```
IF Log Source == WinEventLog
AND EventID == 104
THEN trigger alert "Event Log Cleared"
```
> Attackers clear logs post-exploitation to remove tracks. Event ID 104 = log cleared.

**Use Case 2 — whoami Execution**
```
IF Log Source == WinEventLog
AND EventID == 4688
AND NewProcessName contains "whoami"
THEN trigger alert "WHOAMI Command Execution Detected"
```
> Event ID 4688 = new process created. Attackers run `whoami` after privilege escalation.

> **Why normalization matters:** Detection rules match on specific field-value pairs — unnormalized logs won't have consistent fields to match against.

---

### Alert Investigation Workflow

```
Alert triggered
    ↓
Examine associated events/flows
    ↓
Check which rule conditions were met
    ↓
Determine: True Positive or False Positive?
```

**False Positive actions:**
- Tune the rule to prevent recurrence

**True Positive actions:**
- Investigate further
- Contact asset owner
- Confirm suspicious activity → isolate infected host
- Block suspicious IP
