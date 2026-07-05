# Security Fundamentals

## Know Your Adversary First
Security controls must match the threat.
Protecting against a toddler vs. industrial espionage requires completely different measures.
**No adversary profile = no meaningful security.**

---

## CIA Triad

| Principle | Goal | Failure Example |
|-----------|------|----------------|
| **Confidentiality** | Only authorized parties access data | Credit card data leaked in breach |
| **Integrity** | Data cannot be altered undetected | Attacker changes shipping address on order |
| **Availability** | System accessible when needed | DoS attack takes down shopping site |

> CIA emphasis is context-dependent:
> - University announcement → Integrity critical, Confidentiality low
> - Medical records → All three critical
> - Public website → Availability primary concern

---

## Beyond CIA — Authenticity & Non-repudiation

| Principle | Definition | Example |
|-----------|-----------|---------|
| **Authenticity** | Data/document is genuinely from the claimed source | Verify a purchase order is from a real customer |
| **Non-repudiation** | Source cannot deny being the origin | Customer cannot claim they never placed a 1000-car order |

> These two are interdependent — you need authenticity to establish non-repudiation.
> Critical in: banking, healthcare, legal, e-commerce.

---

## Parkerian Hexad (1998 — Donn Parker)
Extends CIA with two additional elements:

| Element | Definition |
|---------|-----------|
| Availability | System accessible when needed |
| **Utility** | Information is in a usable form |
| Integrity | Data unaltered and detectable if changed |
| Authenticity | Data is from claimed source |
| Confidentiality | Access restricted to authorized parties |
| **Possession** | Authorized parties maintain control of data |

### The Two New Elements Explained

**Utility:**
- Data exists and is available, but is useless in current form
- Example: Encrypted laptop with lost decryption key — data present, zero utility

**Possession:**
- Physical or logical control over data
- Lost when: backup drive stolen, ransomware encrypts your files
- Distinct from confidentiality — attacker can have possession without reading the data

> CIA tells you *what* to protect. Parkerian Hexad tells you *how completely* to think about it.

---

## DAD Triad — Attacks on CIA

| Attack | Targets | Example |
|--------|---------|---------|
| **Disclosure** | Confidentiality | Attacker dumps patient records publicly |
| **Alteration** | Integrity | Attacker modifies patient medication records → wrong treatment |
| **Destruction/Denial** | Availability | Attacker takes down hospital DB → facility can't operate |

```
CIA (Defense)  ←→  DAD (Attack)
Confidentiality    Disclosure
Integrity          Alteration
Availability       Destruction/Denial
```

---

## The CIA Balancing Problem

> Maximizing one principle can undermine another.

| Extreme | Consequence |
|---------|------------|
| Max Confidentiality + Integrity | Availability suffers — too many access controls, system unusable |
| Max Availability | Confidentiality + Integrity suffer — too open, too easy to tamper |

**Good security = balance across all three, not perfection in one.**

> Example: A hospital can't lock down systems so hard that doctors can't access patient records in an emergency. That's a security failure too, just in the availability direction.
