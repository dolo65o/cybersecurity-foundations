# SOC (Security Operations Center) — Fundamentals

## What is a SOC?
- Dedicated facility with a specialized security team
- Monitors an organization's network and resources **24/7**
- Goal: detect suspicious activity and prevent damage before it causes harm

---

## SOC Responsibilities

### Detection

| Type | Description |
|------|-------------|
| **Vulnerabilities** | Weaknesses in software/OS that attackers can exploit; SOC identifies unpatched systems |
| **Unauthorized activity** | Detects illegitimate access (e.g. stolen credentials used to log in) using clues like geo-location anomalies |
| **Policy violations** | Flags breaches of company security rules (e.g. sending confidential files insecurely, pirated downloads) |
| **Intrusions** | Detects unauthorized system/network access — web app exploits, malware infections, etc. |

### Response
- **Incident response support**: Once an incident is detected → minimize impact + perform root cause analysis
- SOC team assists the incident response team throughout the process

---

## Three Pillars of a SOC

<img width="825" height="801" alt="pillers" src="https://github.com/user-attachments/assets/2089e671-31ba-4499-b94e-d44038c144e3" />


A mature SOC requires all three to effectively detect and respond to incidents.

---

## SOC Team — People & Roles

> Automation alone isn't enough — security tools generate massive noise (false positives).
> Human analysts are needed to distinguish real threats from irrelevant alerts.

### Hierarchy

```
CISO
 └── SOC Manager
      ├── SOC Analyst (Level 1)
      ├── SOC Analyst (Level 2)
      ├── SOC Analyst (Level 3)
      ├── Security Engineer
      └── Detection Engineer
```

### Role Breakdown

| Role | Responsibility |
|------|---------------|
| **L1 Analyst** | First responder — basic alert triage, determines if detection is harmful, reports through proper channels |
| **L2 Analyst** | Deeper investigation — correlates data from multiple sources for proper analysis |
| **L3 Analyst** | Experienced — proactively hunts threats, leads containment/eradication/recovery on critical incidents |
| **Security Engineer** | Deploys and configures security solutions used by analysts |
| **Detection Engineer** | Writes detection rules/logic behind security tools (often L2/L3 analysts take this role) |
| **SOC Manager** | Manages SOC processes, liaises with CISO on security posture and team efforts |
| **CISO** | Chief Information Security Officer — top-level security authority in the org |

> **Note:** SOC team size and roles vary depending on organization size and criticality.

---

## SOC Processes

### 1. Alert Triage
First response to any alert. Determines **severity** and **priority** using the **5 Ws**:

| W | Question | Example (Malware on GEORGE PC) |
|---|----------|-------------------------------|
| **What?** | What happened? | Malicious file detected on a host inside the network |
| **When?** | When did it happen? | 13:20 on June 5, 2024 |
| **Where?** | Where was it detected? | Directory of host "GEORGE PC" |
| **Who?** | Who was affected? | User: George |
| **Why?** | Why/how did it happen? | Downloaded from a pirated software site to use software for free |

---

### 2. Reporting
- Harmful alerts are **escalated as tickets** to higher-level analysts
- Report must include: all 5 Ws + thorough analysis + screenshots as evidence

---

### 3. Incident Response & Forensics
- Critical detections trigger a full **incident response** process
- **Forensics** may be performed to determine root cause by analyzing artifacts from the system/network

---

## SOC Technology — Security Solutions

> People + Process alone aren't enough. Technology centralizes device/app data and automates detection & response.

### Core Tools

| Tool | Full Name | Role |
|------|-----------|------|
| **SIEM** | Security Information and Event Management | Collects logs from all network devices, correlates them against detection rules, alerts on matches. Modern SIEMs add user behavior analytics + threat intelligence + ML |
| **EDR** | Endpoint Detection and Response | Real-time + historical visibility into endpoint activity; supports automated response and detailed investigation |
| **Firewall** | — | Barrier between internal/external network; monitors + filters traffic; blocks suspicious traffic before it enters the network |

> **Note:** SIEM provides **detection only** — not response.

### Other SOC Technologies
`Antivirus` `EPP` `IDS/IPS` `XDR` `SOAR` and more

> Tool selection depends on the organization's **threat surface** and **available resources**.
