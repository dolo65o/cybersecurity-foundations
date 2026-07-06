## Cryptographic Failures — OWASP Detail

### What Counts as a Cryptographic Failure
- Passwords stored without hashing (plaintext in DB)
- Weak/broken algorithms: MD5, SHA-1, DES
- "Rolling your own crypto" — custom encryption instead of vetted standards
- Exposed encryption keys (hardcoded, in repos, in config files)
- Data unencrypted in transit (HTTP instead of HTTPS)

> "Rolling your own crypto" is almost always a disaster.
> You are not smarter than the cryptographers who spent decades
> designing and breaking AES, ChaCha20, and bcrypt. Use their work.

---

### Password Hashing — Use Slow Hashes

| Algorithm | Use for | Why |
|-----------|---------|-----|
| **bcrypt** | Passwords | Slow by design — brute force expensive |
| **scrypt** | Passwords | Memory-hard — resists GPU attacks |
| **Argon2** | Passwords | Winner of Password Hashing Competition — current best practice |
| MD5 / SHA-1 | Never for passwords | Fast = crackable in seconds with modern hardware |

---

### Secret Management — Non-Negotiable Rules
```
 Never: hardcode secrets in source code
 Never: store secrets in config files committed to repos
 Never: push .env files to GitHub

 Use: AWS KMS, Azure Key Vault, HashiCorp Vault
 Use: Environment variables injected at runtime
 Use: Secret scanning in CI/CD (detect before merge)
```

> If your secret has ever touched a git commit, rotate it. Now.
> GitHub's secret scanning finds these in minutes. Attackers do too.

---

## Injection Attacks — OWASP

### What It Is
Application takes user input and passes it **directly** into a system that executes it.
Root cause: failure to treat user input as untrusted data.

---

### Common Injection Types

| Type | Target | Example |
|------|--------|---------|
| **SQL Injection** | Database | `' OR 1=1--` in login form |
| **Command Injection** | OS shell | `;rm -rf /` passed to a system call |
| **SSTI** | Template engine | `{{7*7}}` rendered as `49` by Jinja2 |
| **Prompt Injection** | LLM/AI | User input hijacks system prompt context |

> Still on OWASP Top 10 in 2025 — twice. That means devs are still getting this wrong at scale after 20+ years. There's no excuse.

---

### Prevention

| Control | What it fixes |
|---------|--------------|
| **Parameterized queries / prepared statements** | SQL injection — input never touches query structure |
| **Avoid shell-invoking functions** | Command injection — use safe APIs instead |
| **Input validation** | Reject unexpected types, lengths, characters at entry |
| **Output escaping** | SSTI — escape before rendering in templates |
| **Separate system prompts from user input** | Prompt injection — never blend contexts |
| **Allowlists over blocklists** | Define what's valid, reject everything else |

---

### The Core Fix — SQL Example

```python
# WRONG — string concatenation = SQLi waiting to happen
query = "SELECT * FROM users WHERE username = '" + username + "'"

# RIGHT — parameterized query
cursor.execute("SELECT * FROM users WHERE username = ?", (username,))
```

Input never touches query logic. Database treats it as pure data, not executable code.

---

### Hard Truth
> Every injection vulnerability is a developer who trusted user input.
> "Sanitizing" with regex or blocklists is not enough — attackers have decades
> of bypass techniques. Parameterized queries and safe APIs are non-negotiable.
> If you're still building SQL queries with string concatenation in 2025,
> you're not a junior mistake — you're a liability.

---

## Software & Data Integrity Failures — OWASP

### What It Is
Application **blindly trusts** code, updates, or data without verifying they haven't been tampered with.
Related to supply chain failures — but specifically about the **integrity verification** gap.

---

### What Counts as a Failure

| Scenario | Problem |
|----------|---------|
| Auto-installing updates without checksum verification | Tampered update runs as trusted code |
| Loading scripts/configs from unverified external sources | Attacker controls what your app executes |
| Accepting binaries/JSON/templates without signature checks | Malicious data manipulates app logic |
| CI/CD pipeline with no integrity controls | Build artifact tampered between build and deployment |
| Deserializing untrusted data without validation | Malicious payload executes during deserialization |

---

### The Core Problem
```
App assumes: "this update/data came from where it says it did"
Attacker knows: "no one is checking — I can modify it in transit"
```

---

### Prevention

| Control | What it addresses |
|---------|-----------------|
| **Cryptographic checksums** on update packages | Verify file hasn't been altered |
| **Code signing** for binaries and artifacts | Confirm source is who they claim to be |
| **Trusted sources only** for scripts/configs | No CDN scripts without SRI hashes |
| **Subresource Integrity (SRI)** for CDN assets | Browser verifies script hash before executing |
| **Lock down CI/CD pipelines** | Prevent artifact tampering between build and deploy |
| **Validate + sanitize deserialized data** | No blind trust in incoming serialized objects |

---

### SRI Example (Frontend)
```html
<!-- Without SRI — trust whatever the CDN sends -->
<script src="https://cdn.example.com/lib.js"></script>

<!-- With SRI — browser rejects if hash doesn't match -->
<script src="https://cdn.example.com/lib.js"
        integrity="sha384-abc123..."
        crossorigin="anonymous"></script>
```

> If the CDN is compromised and serves a modified script, SRI blocks it.
> Without it, your users execute whatever the attacker put there.

---

### Honest Assessment
This category appears **twice** across OWASP's last two releases for a reason.
Devs are still auto-pulling dependencies, auto-deploying from unverified builds,
and loading third-party scripts with zero integrity checks.
The SolarWinds attack was this exact failure at enterprise scale.
If you're not verifying what you're running, you're not running your code — you're running whoever tampered with it.
