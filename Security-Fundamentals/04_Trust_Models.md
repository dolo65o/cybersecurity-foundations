## Trust Models in Security

### Trust but Verify
- Trust entities (users, systems) but **always log and review** their actions
- Problem: manually verifying everything is impossible at scale
- Solution: automated tools do the heavy lifting

**Requires:**
`Proxy` `IDS` `IPS` `SIEM` `Audit logs`

---

### Zero Trust
- Treats trust itself as a vulnerability
- **"Never trust, always verify"** — every entity is adversarial until proven otherwise
- No implicit trust based on network location or device ownership (kills "trusted internal network" assumption)
- Every resource access requires: **Authentication + Authorization**

**Key benefit:** Breach containment — compromised entity has minimal blast radius

**Implementation — Microsegmentation:**
- Network segments shrink down to single-host level
- Segment-to-segment communication requires explicit auth + ACL checks
- Lateral movement becomes significantly harder

---

### Comparison

| | Trust but Verify | Zero Trust |
|-|-----------------|------------|
| **Default stance** | Trust, then check | Never trust |
| **Insider threat** | Partially addressed | Directly targets it |
| **Complexity** | Lower | Higher |
| **Breach containment** | Moderate | Strong |

---

### Practical Reality
> Zero trust can't be applied 100% without breaking business operations.
> Apply as much as feasible — partial zero trust is still better than none.

---

## Vulnerability, Threat & Risk

### Definitions

| Term | Definition |
|------|-----------|
| **Vulnerability** | A weakness in a system that can be exploited |
| **Threat** | A potential danger that could exploit that vulnerability |
| **Risk** | Likelihood of the threat being exploited × impact on the business |

```
Vulnerability + Threat Actor = Risk
```

---

### Examples

**Physical:**
```
Vulnerability: Glass doors/windows (breakable)
Threat:        Someone could smash them
Risk:          How likely is a break-in? What's the financial/reputational impact?
```

**Information System:**
```
Vulnerability: Hospital database has a known flaw
Threat:        Proof-of-concept exploit is publicly available (threat is REAL)
Risk:          High likelihood + patient data exposure = critical risk → act immediately
```

---

### Why the Distinction Matters

> A vulnerability with no known threat actor = lower risk.
> A vulnerability with a working public exploit = critical risk — patch now.

**Risk drives decisions** — not vulnerability count alone.
A system with 100 low-risk vulns may be safer than one with 1 critical unpatched RCE.
