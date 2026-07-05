## IAAA — Identity, Authentication, Authorization, Accountability

### The Four Layers (sequential — can't skip)

| Layer | What it is | Example |
|-------|-----------|---------|
| **Identity** | Unique representation of a user/service | Username, email, user ID |
| **Authentication** | Proving the identity is genuine | Password, OTP, passkey, biometric |
| **Authorization** | What the authenticated identity is allowed to do | Role-based access, permissions, ACLs |
| **Accountability** | Logging who did what, when, and from where | Audit logs, SIEM alerts |

```
No Identity → can't Authenticate
No Authentication → can't Authorize
No Authorization → can't enforce Accountability meaningfully
```

---

### Why IAAA Failures Are Critical
Failures map directly to OWASP Top 10:2025 categories:

| Failure | Impact |
|---------|--------|
| Broken Authentication | Attacker proves a false identity — accesses another user's data |
| Broken Authorization | Attacker gains more privileges than allowed — privilege escalation |
| Insufficient Accountability | No audit trail — breach goes undetected, no forensic evidence |

---

### Real Consequence
> IAAA failures don't just affect the compromised account.
> They allow **horizontal movement** (access other users' data)
> and **vertical movement** (escalate to admin/higher privileges).
> Both are catastrophic in any system handling sensitive data.

---

## Broken Access Control & IDOR

### What is Broken Access Control?
Server fails to enforce **who can access what** on every request.
Root cause: application **trusts client-supplied input** (URLs, parameters, cookies) without server-side validation.

---

### IDOR — Insecure Direct Object Reference
Most common form of broken access control.
User-controlled input directly references internal objects (DB records, files, accounts).

**Example:**
```
Legitimate:  https://site.com/account?id=7   → your account
Manipulated: https://site.com/account?id=6   → someone else's account
```
If that works → IDOR confirmed → access control is broken.

---

### Privilege Escalation Types

| Type | Description | Example |
|------|-------------|---------|
| **Horizontal** | Same role, different user's data | Viewing another customer's order |
| **Vertical** | Lower role accessing higher-privilege functions | Regular user accessing admin panel |

---

### Practical — accountID Enumeration

**Approach:**
```
Start at id=1, increment manually or with Burp Intruder
Check account balance in each response
Flag any account with balance > $1,000,000
```

**Burp Suite approach:**
```
Capture request → Send to Intruder
Set §accountID§ as payload position
Payload: Numbers 1–100 (or higher)
Start attack → sort/filter responses by balance value
```

---

### Why This Happens
- Developer checks login ✓ but not ownership ✗
- "Is the user logged in?" ≠ "Does this user own this resource?"
- Both checks are required on **every request**, not just at login

---

### IDOR Variations to Know
| Variant | How it's obscured |
|---------|-----------------|
| Sequential IDs | `?id=6` → `?id=7` (trivial) |
| Encoded IDs | Base64: `?id=Ng==` → decode, change, re-encode |
| Hashed IDs | MD5/SHA of userID — predictable if input is guessable |
| GUIDs | Harder but sometimes leaked in other responses |

> Encoding ≠ security. Base64 is not encryption. Always check if IDs are just obscured, not protected.

---

## Authentication Failures

### What is it?
Application cannot reliably **verify or bind a user's identity**.
Results in: logging in as another user, session hijacking, or account takeover.

---

### Common Authentication Weaknesses

| Weakness | Description |
|----------|-------------|
| **Username enumeration** | App reveals if a username exists ("user not found" vs "wrong password") |
| **Weak/guessable passwords** | No complexity requirements, no lockout, no rate limiting |
| **Logic flaws in auth flow** | Registration/login process has exploitable gaps |
| **Insecure session/cookie handling** | Predictable tokens, no expiry, not tied to user identity properly |

---

### Attack — Username Collision (Case Insensitivity Flaw)

**Vulnerability:** Application treats `admin` and `aDmiN` as different during registration but same during login.

**Steps:**
```
1. Register new account with username: aDmiN
2. Set any password you control
3. Log in with: aDmiN + your password
4. Application normalizes to lowercase → logs you in as: admin
5. You now have admin's session
```

**Root cause:**
```
Registration check: case-sensitive   → "aDmiN" ≠ "admin" → allows registration
Login lookup:       case-insensitive → "aDmiN" == "admin" → returns admin's account
Session bound to:   admin's account
```
Inconsistent string comparison between registration and authentication = account takeover.

---

### Why This Happens
Developers forget that **every step of the auth flow must apply the same normalization rules**.
If login lowercases input but registration doesn't → attacker exploits the gap.

**Fix:**
```
Normalize username (lowercase/trim) at registration time
Store normalized form in DB
Apply same normalization on every lookup
```

---

### Other Logic Flaw Examples to Know

| Flaw | Attack |
|------|--------|
| Password reset sends token in URL | Token leaked via Referer header

---

## Security Logging & Monitoring Failures

### Why It Matters
No logs = no detection, no investigation, no accountability.
Attackers rely on poor logging to operate undetected and cover tracks.

---

### Common Logging Failures

| Failure | Impact |
|---------|--------|
| Missing auth events (login success/fail) | Can't detect brute force or credential stuffing |
| Vague error messages in logs | Can't reconstruct what actually happened |
| No alerting on brute-force / privilege changes | Attacks run undetected indefinitely |
| Short log retention | Evidence gone before investigation starts |
| Logs stored where attacker can reach them | Attacker deletes or modifies their tracks |
| No centralized logging | Logs exist but no one correlates them |

---

### What Good Logs Must Capture

| Field | Why |
|-------|-----|
| **Who** | User ID, IP address, session token |
| **What** | Action performed, resource accessed |
| **When** | Precise timestamp (UTC) |
| **Where** | Source IP, endpoint, geographic location |
| **Outcome** | Success / failure / error code |

---

### Log Investigation — What to Look For

**Brute force pattern:**
```
Multiple failed logins → same IP, different usernames = credential stuffing
Multiple failed logins → same username, different IPs = distributed brute force
```

**Privilege escalation:**
```
User role change events
Access to admin endpoints by non-admin accounts
```

**Suspicious timing:**
```
Logins at 3AM from unusual geolocation
Bulk data access in short timeframe = exfiltration
```

---

### The Hard Truth
> If key log fields are missing, you can't answer:
> - Who attacked? (no IP/user)
> - What did they access? (no resource logging)
> - When did it start? (no timestamps)
> - Did they succeed? (no outcome logging)

**Missing logs don't just slow investigation — they make it impossible.**
This is why logging is a security control, not an afterthought.

---

### Logging Best Practices
- Store logs **off the compromised system** (remote/centralized SIEM)
- Make logs **tamper-evident** (append-only, signed)
- Retain for minimum **90 days** (1 year for compliance-heavy environments)
- Alert on: repeated failures, privilege changes, impossible travel, off-hours access
