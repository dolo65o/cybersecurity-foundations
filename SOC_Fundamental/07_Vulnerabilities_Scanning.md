## Vulnerabilities & Patching

### What is a Vulnerability?
A weakness in software or hardware that an attacker can exploit to compromise a system.

> Analogy: Small holes in a roof — harmless looking but cause serious damage if ignored.

### Key Difference from Physical Weaknesses
- Physical vulnerabilities (roof holes) are visible
- Digital vulnerabilities are **hidden** — require dedicated hunting to discover
- Attackers actively search for them before defenders find them

### Patching
The process of applying fixes to close discovered vulnerabilities.

```
Vulnerability discovered → Patch developed → Patch applied → System protected
```

> Unpatched vulnerabilities = open door for attackers. The longer a vulnerability stays unpatched, the higher the risk.

---

## Vulnerability Scanning

### Why Scan Regularly?
- Attackers actively hunt for vulnerabilities before defenders find them
- Manual scanning is slow and misses things — automated tools are standard
- Required by many compliance/regulatory frameworks (quarterly or annually)

**Automated scanner workflow:**
```
Provide IP / network range → Scanner runs → Report generated with findings
```

---

### Scan Types

#### Authenticated vs Unauthenticated

| | Authenticated | Unauthenticated |
|-|--------------|-----------------|
| **Credentials required?** | Yes | No (IP only) |
| **Perspective** | Inside the host | Outside the host |
| **Depth** | Deep — config, installed apps, internal exposure | Surface-level — external exposure only |
| **Use case** | Internal DB scan with credentials | Public-facing website scan |

#### Internal vs External

| | Internal | External |
|-|----------|----------|
| **Conducted from** | Inside the network | Outside the network |
| **Finds** | Vulnerabilities exposed after attacker gets in | Vulnerabilities exposed to outside attackers |
| **Simulates** | Post-breach attacker | External threat actor |

---

### Key Terms
| Term | Definition |
|------|-----------|
| **Vulnerability** | Weakness in software/hardware |
| **Patch** | Fix applied to close a vulnerability |
| **Threat surface** | Total area exposed to potential attack |

---

## Vulnerability Scanners — Overview

| Tool | Type | Deployment | Key Features |
|------|------|-----------|-------------|
| [**Nessus**](https://www.tenable.com/products/nessus) | Free + Paid (Tenable) | On-premises | Extensive scan options; unlimited scans + professional support in paid version |
| [**Qualys**](https://qualys.com/) | Subscription | Cloud-based | Continuous scanning, compliance checks, asset management, auto-alerts; no hardware overhead |
| [**Nexpose**](https://www.rapid7.com/products/nexpose/) | Subscription (Rapid7) | On-premises / Hybrid | Discovers new assets automatically; risk scores based on asset value + vuln impact; compliance checks |
| [**OpenVAS**](https://www.openvas.org/)| Open-source (Greenbone) | On-premises | Basic scanning against known vuln DB; good for small orgs and individuals |

---

### Vulnerability Scan Reports
All major scanners generate reports containing:
- List of discovered vulnerabilities
- Risk scores
- Detailed descriptions
- Remediation methods (advanced scanners)
- Export in multiple formats

---

### Choosing a Scanner — Factors to Consider
`Scope` · `Available resources` · `Depth of analysis required` · `Budget` · `Deployment preference (cloud vs on-prem)`

---

## CVE & CVSS

### CVE — Common Vulnerabilities and Exposures
A unique identifier assigned to every publicly discovered vulnerability.
Developed by **MITRE Corporation**.

**CVE Number Format:**
```
CVE - 2024 - 9374
 ↑      ↑      ↑
Prefix  Year  Arbitrary digits (4+)
```

- Published in the CVE database for public awareness
- Allows tracking and referencing specific vulnerabilities
- Search any known vulnerability [hear](https://cve.mitre.org)

---

### CVSS — Common Vulnerability Scoring System
A severity score (0–10) assigned to each vulnerability based on impact, exploitability, and other factors.
Used to **prioritize** which vulnerabilities to patch first.

| CVSS Score | Severity |
|-----------|---------|
| 0.0 – 3.9 | Low |
| 4.0 – 6.9 | Medium |
| 7.0 – 8.9 | High |
| 9.0 – 10.0 | Critical |

---

### CVE vs CVSS

| | CVE | CVSS |
|-|-----|------|
| **Purpose** | Uniquely identify a vulnerability | Score its severity |
| **Format** | CVE-YEAR-DIGITS | 0.0 to 10.0 |
| **Use** | Reference/tracking | Prioritization |

---

## OpenVAS — Installation & Vulnerability Scan

### Installation (via Docker)

```bash
# Install Docker
sudo apt install docker.io

# Run OpenVAS container (Immauss image)
sudo docker run -d -p 443:443 --name openvas immauss/openvas
```

> Docker containers bundle all dependencies — avoids OpenVAS's hectic native install process.

### Access Web Interface
```
https://127.0.0.1
```
Log in with credentials → reach OpenVAS dashboard

<img width="1280" height="645" alt="1" src="https://github.com/user-attachments/assets/0a476b42-9adc-4b64-9f90-c69d17d971b7" />


---

### Performing a Scan — Workflow


Dashboard
  → Scans → Tasks

<img width="2352" height="1256" alt="2" src="https://github.com/user-attachments/assets/4fd91b07-7953-48d6-8272-2143aa7b8a3f" />


  → New Task (star icon)

<img width="2316" height="1286" alt="3" src="https://github.com/user-attachments/assets/102fb204-cc82-4974-9bed-5e2a60770ca3" />

  
      → Enter task name
      → Scan Targets → enter target name + IP → Create

<img width="2470" height="1104" alt="4" src="https://github.com/user-attachments/assets/0bb79302-ffa3-4854-9e5e-b6b6e4d8bc23" />

      → Select scan type → Create

<img width="2310" height="1274" alt="5" src="https://github.com/user-attachments/assets/01f21cc1-5590-4005-b493-3a5253be1a4b" />

     
  → Click Play (▶) on the task to start scan

<img width="2306" height="1280" alt="6" src="https://github.com/user-attachments/assets/28343753-deb6-4bd0-9c70-4b07b013efce" />

  → Wait for status: "Done"
  
  → Click task name → view vulnerability count

<img width="2300" height="1152" alt="7" src="https://github.com/user-attachments/assets/ccd89679-affa-44ff-b240-e7184baad834" />

  → Click count → view full vulnerability list (with severity)

<img width="2308" height="1156" alt="8" src="https://github.com/user-attachments/assets/81cd34ea-b5bc-4c65-b9dd-123bd381f98c" />

  → Click individual vulnerability → view details
  
<img width="2478" height="1234" alt="9" src="https://github.com/user-attachments/assets/68099154-b2b6-40d9-aa45-0fc2dd78b7e9" />


