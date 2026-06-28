## Firewall — Introduction

### What is a Firewall?
A security solution that **inspects incoming and outgoing network traffic** and allows or denies it based on configured rules.

> Analogy: A security guard at a building entrance — checks everyone coming in/going out and blocks unauthorized access.

### How it Works
```
Internet ↔ Firewall (checks rules) ↔ Your device/network
```
- Every packet entering or leaving must pass through the firewall first
- Firewall checks the packet against its ruleset → **Allow** or **Deny**
- Modern firewalls go beyond simple rule-based filtering (more features covered next)

---

## Firewall Types

### Comparison Table

| Type | OSI Layer | Key Characteristics |
|------|-----------|-------------------|
| **Stateless** | L3–L4 | No connection tracking; matches every packet against rules independently; fast but limited |
| **Stateful** | L3–L4 | Tracks connection state in a state table; auto-allows/denies future packets based on history |
| **Proxy (App-level Gateway)** | L7 | Inspects packet contents; acts as intermediary; masks internal IPs; content filtering |
| **NGFW** | L3–L7 | Deep packet inspection + IPS + heuristic analysis + SSL/TLS decryption + threat intel correlation |

---

### Key Differences

**Stateless vs Stateful:**
- Stateless forgets every packet — treats each one as new, even from a previously blocked source
- Stateful remembers — once a source is blocked, all future packets from it are auto-denied

**Stateful vs Proxy:**
- Stateful inspects headers (IP, port) only
- Proxy inspects actual packet **contents** + provides application control

**Proxy vs NGFW:**
- Both do deep inspection and SSL/TLS decryption
- NGFW adds **IPS**, **heuristic analysis**, and **threat intelligence feeds** — most comprehensive

---

### When to Use Which

| Use Case | Best Fit |
|----------|---------|
| High-speed network, basic filtering | Stateless |
| Connection-aware filtering | Stateful |
| Content filtering, anonymity | Proxy |
| Advanced threat protection | NGFW |

---

## Firewall Rules

### Rule Components

| Field | Description |
|-------|-------------|
| **Source Address** | IP of the machine originating the traffic |
| **Destination Address** | IP of the machine receiving the traffic |
| **Port** | Port number for the traffic |
| **Protocol** | TCP / UDP / etc. |
| **Action** | Allow / Deny / Forward |
| **Direction** | Inbound / Outbound |

---

### Actions

#### Allow
Permits the defined traffic.
| Action | Source | Destination | Protocol | Port | Direction |
|--------|--------|-------------|----------|------|-----------|
| Allow | 192.168.1.0/24 | Any | TCP | 80 | Outbound |
> Allow all outgoing HTTP traffic from internal network

#### Deny
Blocks the defined traffic.
| Action | Source | Destination | Protocol | Port | Direction |
|--------|--------|-------------|----------|------|-----------|
| Deny | Any | 192.168.1.0/24 | TCP | 22 | Inbound |
> Block all incoming SSH to critical server

#### Forward
Redirects traffic to a different network segment (firewall must support routing).
| Action | Source | Destination | Protocol | Port | Direction |
|--------|--------|-------------|----------|------|-----------|
| Forward | Any | 192.168.1.8 | TCP | 80 | Inbound |
> Forward all incoming HTTP traffic to web server at 192.168.1.8

---

### Rule Directionality

| Type | Applies To | Example |
|------|-----------|---------|
| **Inbound** | Incoming traffic only | Allow HTTP (port 80) to web server |
| **Outbound** | Outgoing traffic only | Block SMTP (port 25) from all except mail server |
| **Forward** | Traffic routed inside network | Forward port 80 traffic to internal web server |

---
## Windows Defender Firewall

### Overview
Built-in Windows firewall. Open via: `Start → "Windows Defender Firewall"`

### Network Profiles
| Profile | When Applied |
|---------|-------------|
| **Private** | Home/trusted network |
| **Public/Guest** | Coffee shops, restaurants, untrusted networks |

> Windows auto-selects profile using **Network Location Awareness (NLA)**. Different rules can be set per profile.

---

### Main Dashboard Options
| Option | Purpose |
|--------|---------|
| Allow/disallow apps | Checkmark apps to allow per network profile |
| Turn on/off | Enable or disable firewall (Microsoft recommends keeping ON) |
| Block all incoming | Stricter option instead of fully disabling |
| Restore Defaults | Resets all firewall settings to default |

---

### Creating a Custom Outbound Rule
**Goal:** Block all outgoing HTTP (port 80) and HTTPS (port 443) traffic

**Steps:**
```
Advanced Settings
→ Outbound Rules → New Rule
→ Type:     Custom
→ Programs: All programs
→ Protocol: TCP
→ Remote Port: Specific ports → 80,443
→ Scope:    Default (any IP)
→ Action:   Block the connection
→ Profile:  All (Domain, Private, Public)
→ Name:     e.g. "Block HTTP HTTPS Outbound"
→ Finish
```

> **Test:** Try browsing any website after rule creation → should fail with "can't reach this page"

---

### Rule Types Available
- **Inbound Rules** — control incoming traffic
- **Outbound Rules** — control outgoing traffic
- Both accessible under `Advanced Settings`

---

## Linux Firewall — Netfilter & ufw

### Linux Firewall Stack
```
ufw / firewalld / iptables / nftables
            ↓
        Netfilter (kernel framework)
```

**Netfilter** — core Linux kernel framework providing: packet filtering, NAT, connection tracking

### Firewall Utilities

| Utility | Notes |
|---------|-------|
| **iptables** | Most widely used; complex syntax |
| **nftables** | Successor to iptables; enhanced filtering + NAT |
| **firewalld** | Predefined rule sets; zone-based configuration |
| **ufw** | Beginner-friendly wrapper over iptables |

---

### ufw — Common Commands

```bash
# Check status
sudo ufw status

# Enable / disable
sudo ufw enable
sudo ufw disable

# Default policies
sudo ufw default allow outgoing
sudo ufw default deny incoming

# Allow/deny specific port+protocol
sudo ufw allow 22/tcp       # allow SSH
sudo ufw deny 22/tcp        # block SSH

# List all rules (numbered)
sudo ufw status numbered

# Delete a rule by number
sudo ufw delete 2
```

### Example Output
```
# After: sudo ufw status numbered
     To          Action      From
     --          ------      ----
[ 1] 22/tcp      DENY IN     Anywhere
[ 2] 22/tcp(v6)  DENY IN     Anywhere (v6)

# After: sudo ufw delete 2
Deleting: deny 22/tcp
Proceed with operation (y|n)? y
Rule deleted (v6)
```

> `default` policy applies to all traffic unless overridden by a specific rule
