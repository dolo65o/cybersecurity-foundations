## SOC — Events

### How Events Become Alerts
- Every process on a device generates **events** (interactive + background)
- Events are ingested into security solutions as **logs**
- Security solution detects patterns → triggers **alerts**
- Security team then analyzes those alerts

**Example processes generating events:**
`Explorer.exe` `Lsass.exe` `Svchost.exe` `Wininit.exe`

---

### False Positive vs True Positive

| Type | Definition | Example |
|------|-----------|---------|
| **False Positive** | Alert triggered but activity is harmless | Large data transfer flagged → was actually a cloud backup |
| **True Positive** | Alert triggered and activity is actually harmful | Phishing email alert → confirmed malicious email targeting a user |

> True positives are classified as **Incidents**

---

### Incident Severity Levels
Priority order: **Critical → High → Medium → Low**

| Severity | Handle first? |
|----------|--------------|
| Critical | Yes — highest priority |
| High | Second |
| Medium | Third |
| Low | Last |

> False positive alerts are **discarded** — not escalated

---

## Security Incident Types

| Incident | Description | Key Note |
|----------|-------------|----------|
| **Malware Infection** | Malicious program damages system/network/app; spread via files (docs, executables, text) | Most common incident type |
| **Security Breach** | Unauthorized access to confidential data | Critical for businesses — data must stay accessible only to authorized users |
| **Data Leak** | Confidential data exposed to unauthorized entities; used for reputational damage or extortion | Can be **unintentional** (human error, misconfiguration) — unlike breaches |
| **Insider Attack** | Attack initiated from within the org by an employee/insider | More dangerous — insiders have greater resource access than outsiders |
| **DoS Attack** | Floods system/network/app with fake requests → exhausts resources → legitimate users can't access it | Targets **Availability** (one of the 3 pillars of cybersecurity: CIA) |

---

### Severity is Context-Dependent
> The same incident can be catastrophic for one org and minor for another.

**Example:**
- XYZ Corp → data leak = minor (data is useless to others)
- XYZ Corp → DoS on primary website = massive loss (business depends on it)

> Never compare incident types by severity in isolation — **always consider the target's context**

---

## Incident Response Frameworks — SANS & NIST

### Framework Comparison

| SANS | NIST |
|------|------|
| Preparation | Preparation |
| Identification | Detection and Analysis |
| Containment | Containment, Eradication, and Recovery |
| Eradication | ↑ (combined above) |
| Recovery | ↑ (combined above) |
| Lessons Learned | Post Incident Activity |

> SANS mnemonic: **PICERL** (Preparation, Identification, Containment, Eradication, Recovery, Lessons Learned)

---

### SANS 6 Phases — Detail

| Phase | What happens | Example |
|-------|-------------|---------|
| **Preparation** | Build IR teams, create IR plan, deploy security solutions | Employee phishing awareness training |
| **Identification** | Detect abnormal behavior using security tools/monitoring | Large outbound data transfer detected → traced to phishing attachment |
| **Containment** | Minimize impact — isolate victim machine, disable compromised accounts | Host isolated from network to stop lateral movement |
| **Eradication** | Remove the threat completely from the environment | Deep malware scan run to clean the host |
| **Recovery** | Restore systems from backup or rebuild; test before returning to use | Host reconfigured, exfiltrated data restored from backup |
| **Lessons Learned** | Document gaps in detection/response; improve process for future | Post-incident review meeting to analyze root cause |

---

### Incident Response Plan (IRP)
Formal document approved by senior management. Covers procedures before, during, and after an incident.

**Key components:**
- Roles and responsibilities
- IR methodology
- Communication plan (including law enforcement)
- Escalation path

---

## Playbooks & Runbooks

### Playbook
High-level guidelines for responding to a specific incident type.

**Example — Phishing Email Playbook:**
1. Notify all stakeholders of the phishing incident
2. Analyze email headers and body to confirm if malicious
3. Check for attachments and analyze them
4. Determine if anyone opened the attachments
5. Isolate infected systems from the network
6. Block the sender

---

### Runbook
Detailed step-by-step execution instructions for specific steps within a playbook.
Steps may vary based on available tools and resources.

---

### Key Difference

| | Playbook | Runbook |
|-|----------|---------|
| **Level** | High-level guidelines | Granular execution steps |
| **Scope** | Entire incident type | Specific task within the response |
| **Analogy** | "What to do" | "Exactly how to do it" |
