## Security Models

### Bell-LaPadula — Confidentiality Model

**Core rule: "Write up, Read down"**

| Property | Rule | Purpose |
|----------|------|---------|
| Simple Security | No read up | Lower clearance can't read higher classified data |
| Star Security | No write down | Higher clearance can't write to lower level (prevents leaking) |
| Discretionary | Access matrix | Explicit per-subject, per-object permissions |

**Access Matrix Example:**
| Subject | Object A | Object B |
|---------|----------|----------|
| Subject 1 | Write | No access |
| Subject 2 | Read/Write | Read |

**Limitation:** Not designed for file sharing.

---

### Biba — Integrity Model

**Core rule: "Read up, Write down"** (opposite of Bell-LaPadula)

| Property | Rule | Purpose |
|----------|------|---------|
| Simple Integrity | No read down | High integrity subject won't be contaminated by low integrity data |
| Star Integrity | No write up | Low integrity subject can't corrupt high integrity data |

**Limitation:** Doesn't handle insider threats.

---

### Clark-Wilson — Integrity Model

More practical than Biba. Uses formal procedures to enforce integrity.

| Concept | What it is |
|---------|-----------|
| **CDI** (Constrained Data Item) | Data whose integrity must be preserved |
| **UDI** (Unconstrained Data Item) | All other data — user input, system input |
| **TP** (Transformation Procedure) | Programmed operations (read/write) that maintain CDI integrity |
| **IVP** (Integrity Verification Procedure) | Checks that CDIs are valid and uncorrupted |

---

### Model Comparison

| Model | Goal | Key Rule | Weakness |
|-------|------|---------|----------|
| Bell-LaPadula | Confidentiality | Write up, read down | No file sharing support |
| Biba | Integrity | Read up, write down | No insider threat handling |
| Clark-Wilson | Integrity | Controlled access via TPs/IVPs | More complex to implement |

### Other Security Models (for further study)
`Brewer-Nash` `Goguen-Meseguer` `Sutherland` `Graham-Denning` `Harrison-Ruzzo-Ullman`

---

## Defence-in-Depth (Multi-Level Security)

### Concept
No single security control is sufficient. Layer multiple controls so that bypassing one doesn't compromise everything.

> A locked drawer means nothing if the room, apartment, and building are all wide open.

### Layered Security Example
```
Building gate (perimeter)
  → Apartment main door
    → Room lock
      → Locked drawer
        → (optional) security cameras throughout
```

### Why It Works
- Stops most attackers at outer layers
- Slows down sophisticated attackers — buys time for detection
- No single point of failure

### In Practice (Network Security)
```
Perimeter Firewall
  → Network IDS/IPS
    → Host-based Firewall
      → Endpoint AV/EDR
        → Application-level controls
          → Data encryption at rest
            → Audit logging + SIEM
```

> **Key point:** Defence-in-depth doesn't make you unbreakable — it makes you harder and slower to compromise, giving defenders time to detect and respond.
