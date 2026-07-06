## Security Misconfigurations

### What It Is
Not a code bug — a **deployment/configuration mistake**.
Systems deployed with unsafe defaults, exposed services, or wrong permissions.

---

### Why It's Dangerous
Complex modern stacks (cloud + APIs + containers + third-party services) = massive misconfiguration surface.
One exposed admin panel or public S3 bucket = full breach, no exploit needed.

**Real example — Uber 2017:**
```
Mistake:  AWS S3 backup bucket set to public
Result:   Anyone could download driver + rider data
Exploit:  Zero — no credentials, no vulnerability, just open storage
```
That's the point. Misconfigs require no hacking skill — just knowing where to look.

---

### Common Misconfiguration Patterns

| Pattern | Risk |
|---------|------|
| Default credentials unchanged | Trivial login to admin panels |
| Unnecessary services exposed | Expanded attack surface |
| Public cloud buckets (S3, Azure Blob, GCP) | Data exfiltration without credentials |
| Missing auth on APIs | Unrestricted data access |
| Verbose error messages | Stack traces reveal tech stack, file paths, DB info |
| Outdated software/containers | Known CVEs = ready-made exploits |
| Exposed AI/ML endpoints | Model theft, prompt injection, data leakage |

---

### Prevention

| Control | What it addresses |
|---------|-----------------|
| Harden defaults, remove unused features | Reduces attack surface |
| Enforce least privilege everywhere | Limits blast radius of misconfiguration |
| Network segmentation | Isolates sensitive resources |
| Patch software + containers regularly | Closes known CVE windows |
| Generic error messages only | No info leakage via stack traces |
| Regular cloud config audits | Catches public buckets, over-permissioned roles |
| Secure AI endpoints | Auth + monitoring on ML APIs |
| Automated config checks in CI/CD pipeline | Catches misconfigs before deployment |

---

### Honest Callout
> Misconfigurations are the most embarrassing class of vulnerability.
> They don't require a sophisticated attacker.
> They require a misconfigured system and someone who knows how to use a browser or `aws s3 ls`.
> Most are caught by automated scanners — which means if you're not running them, someone else will find your mistakes first.

---

## Software Supply Chain Failures

### What It Is
Your code is clean. Your dependencies aren't.
Attackers compromise the **components, libraries, or update pipelines** you trust and ship
malicious code directly into your system — without touching your codebase.

---

### Why It's Particularly Nasty
- You don't write the vulnerable code — you just use it
- Automated updates = automatic compromise delivery
- Affects every downstream user simultaneously
- Hard to detect: malicious code arrives via a "trusted" channel

**Real example — SolarWinds 2021:**
```
Attack vector:  Malicious code injected into Orion software build process
Delivery:       Legitimate, signed software update
Victims:        Thousands of orgs that auto-installed the update
Detection time: Months
```
Zero exploitation needed — the update mechanism did the attacker's job.

---

### Common Patterns

| Pattern | Risk |
|---------|------|
| Unverified/unmaintained libraries | Abandoned libs accumulate unpatched CVEs |
| Auto-install updates without verification | Update = instant compromise delivery |
| Unverified third-party AI models | Hidden backdoors, biased outputs, data leakage |
| Insecure CI/CD pipelines | Build tampering injects malicious artifacts |
| No provenance/license tracking | Can't audit what's actually in your build |
| No post-deployment dependency monitoring | Vuln discovered after deployment — you'd never know |

---

### Protection Measures

| Control | What it addresses |
|---------|-----------------|
| Verify all third-party components before use | Stops compromised packages at intake |
| Monitor + patch dependencies regularly | Closes CVE windows post-deployment |
| Sign + verify software updates | Detects tampered update packages |
| Lock down CI/CD pipelines | Prevents build-time injection |
| Track provenance + licensing | Know exactly what's in your build |
| Runtime monitoring of dependency behavior | Catches compromise after installation |
| Supply chain threat modeling in SDLC | Builds security in from the start |

---

### The AI Supply Chain Problem
Increasingly relevant — using a pre-trained model from an unverified source is the same
risk as using an unverified npm package. The model can:
- Contain embedded backdoors triggered by specific inputs
- Produce biased/manipulated outputs by design
- Leak training data (including PII) through inference

> Treat AI models like code dependencies — verify source, audit behavior, monitor runtime.

---

### Hard Truth
> Most devs check their own code for bugs but blindly `pip install` or `npm install`
> whatever the tutorial says. Your app's security is only as strong as your weakest dependency.
> And you probably have hundreds of them you've never audited.

---

## Cryptographic Failures

### What It Is
Encryption missing, broken, or misconfigured.
Result: sensitive data readable by anyone who intercepts or accesses it.

---

### Common Patterns

| Failure | Problem |
|---------|---------|
| MD5, SHA-1, ECB mode | Weak/broken — easily cracked or reversed |
| Hard-coded secrets in code | Anyone with repo access = full compromise |
| No key rotation | One leaked key = permanent access |
| No encryption at rest/in transit | Plaintext data = free data for attackers |
| Self-signed/invalid TLS certs | MITM attacks trivial |

---

### Attack Vectors
- **MITM** — intercept unencrypted/weak TLS traffic
- **Brute force** — crack weak keys or hashed passwords (MD5/SHA-1)
- **Source code review** — find hard-coded secrets in public repos

---

### Prevention

| Fix | Why |
|-----|-----|
| AES-GCM, ChaCha20, TLS 1.3 | Modern, unbroken algorithms |
| Key management service (AWS KMS, Vault) | No hard-coded secrets |
| Regular key/secret rotation | Limits damage from leaks |
| Encrypt everything sensitive at rest + transit | No plaintext exposure |
| Certificate inventory + monitoring | Catch expired/invalid certs early |

---

## Insecure Design

### What It Is
Not a misconfiguration or a bug — **flawed logic baked into the architecture itself**.
You can't patch your way out of it. The design has to change.

---

### Real Example — Clubhouse
```
Assumption: users only interact via mobile app
Reality:    backend API had no authentication
Result:     anyone could query user data + private conversations directly
Fix needed: full API redesign — not a patch
```

---

### Common Patterns

| Pattern | Problem |
|---------|---------|
| Weak business logic (recovery/approval flows) | Bypass authentication via password reset flaws |
| Flawed user/model behaviour assumptions | System breaks when users don't behave as expected |
| AI components with unchecked authority | LLM can take actions without validation |
| Missing LLM/agent guardrails | Prompt injection, data leakage, hijacked context |
| Debug/test bypasses left in production | Backdoor shipped to prod |
| No abuse-case review | Happy path only — attack paths never considered |

---

### AI-Specific Design Failures (2025 Reality)

| Failure | What happens |
|---------|-------------|
| **Prompt injection** | User input blends with system prompt → attacker hijacks context |
| **Blind trust in model output** | System acts on AI decision without human validation |
| **Poisoned models** | Unverified model has embedded backdoors from training data |

---

### How to Design Securely

**General:**
- Threat model at every stage — not just at kickoff
- Define security requirements per feature before writing code
- Least privilege across users, APIs, services
- Proper auth/authz/session management from the start
- Keep dependencies verified and current

**AI-specific:**
- Treat every model as untrusted until verified
- Separate system prompts from user content — always
- Validate + filter all model inputs and outputs
- Keep sensitive data out of prompts
- Require human review for high-risk AI actions
- Log model provenance + monitor behavior continuously

---

### Hard Truth
> Developers using AI code generation are now shipping insecure design at scale.
> GitHub Copilot doesn't threat model. ChatGPT doesn't know your trust boundaries.
> If you don't review AI-generated code for logic flaws and abuse paths,
> you're outsourcing your security decisions to a model that has no idea what it's building.
