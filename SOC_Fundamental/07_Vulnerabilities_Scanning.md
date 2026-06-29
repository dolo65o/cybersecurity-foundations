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

