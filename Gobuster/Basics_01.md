# Gobuster — Introduction & Overview

## What is Gobuster?
An open-source offensive tool written in **Golang** that brute forces web directories, DNS subdomains, vhosts, Amazon S3 buckets, and Google Cloud Storage using wordlists.

> Sits between **reconnaissance and scanning** phases of ethical hacking. Pre-installed on Kali Linux.

---

## Key Concepts

**Enumeration** — Listing all available resources whether accessible or not.

**Brute Force** — Trying every possibility until a match is found. Like trying all keys on a lock.

---

## Available Commands

| Command | Use |
|---------|-----|
| `dir` | Web directory & file enumeration |
| `dns` | DNS subdomain enumeration |
| `vhost` | Virtual host enumeration |

---

## Common Flags

| Short | Long | Description |
|-------|------|-------------|
| `-t` | `--threads` | Number of threads (default: 10) |
| `-w` | `--wordlist` | Wordlist to use for brute forcing |
| — | `--delay` | Wait time between requests (avoid detection) |
| — | `--debug` | Troubleshoot unexpected errors |
| `-o` | `--output` | Save results to a file |

---

## Example — Directory Enumeration

```bash
gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
```

**Breakdown:**
- `dir` → directory/file enumeration mode
- `-u` → target URL
- `-w` → wordlist to brute force with
- `-t 64` → use 64 threads (faster performance)

> Gobuster takes each wordlist entry, appends it to the URL and sends a GET request e.g. `http://example.thm/images/`

---

## Get Help
```bash
gobuster --help
```
# Gobuster — dir Mode

## What is dir Mode?
Enumerates **website directories and files** by brute forcing with a wordlist. Returns HTTP status codes to tell you if a directory is accessible or not.

> Websites follow common directory structures (e.g. WordPress)
> making them predictable and susceptible to brute force.

```
html/
└── wordpress/
    ├── wp-admin
    ├── wp-content
    └── wp-includes
```

---

## Basic Syntax
```bash
gobuster dir -u "http://www.example.thm" -w /path/to/wordlist
```
> `-u` and `-w` are **required** for dir mode to work

---

## dir Mode Flags

| Short | Long | Description |
|-------|------|-------------|
| `-c` | `--cookies` | Pass a cookie (e.g. session ID) with each request |
| `-x` | `--extensions` | Scan for specific file types e.g. `.php,.js` |
| `-H` | `--headers` | Add custom headers to each request |
| `-k` | `--no-tls-validation` | Skip TLS cert check (useful for CTFs with self-signed certs) |
| `-n` | `--no-status` | Hide status codes — cleaner output |
| `-P` | `--password` | Password for authenticated requests |
| `-U` | `--username` | Username for authenticated requests |
| `-s` | `--status-codes` | Show only specific status codes e.g. `200` or `300-400` |
| `-b` | `--status-codes-blacklist` | Hide specific status codes (overrides `-s`) |
| `-r` | `--followredirect` | Follow redirect responses (301/302) |

---

## Examples

### Basic directory scan
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```
- `dir` → directory enumeration mode
- `-u` → base URL to scan (must include `http://` or `https://`)
- `-w` → wordlist — each entry appended to URL
- `-r` → follow redirects (301/302)

### Scan for specific file types
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt \ -x .php,.js
```
> Finds directories AND files ending in `.php` or `.js`

---

## Important Notes

- URL **must include protocol** (`http://` or `https://`) — scan fails without it
- Use **HOSTNAME** over IP when possible — one IP can host multiple sites (virtual hosting)
- Gobuster does **NOT enumerate recursively** — if you find `/admin/`, run a separate scan on it
- Use `-k` on CTF/THM machines with self-signed HTTPS certificates

---

## Get Help
```bash
gobuster dir --help
```

---

# Gobuster — dns Mode

## What is dns Mode?
Brute forces **DNS subdomains** of a target domain.

> Just because the main domain is patched doesn't mean subdomains are too. e.g. `tryhackme.thm` may be secure but `mobile.tryhackme.thm` may have vulnerabilities.

---

## Basic Syntax
```bash
gobuster dns -d example.thm -w /path/to/wordlist
```
> `-d` and `-w` are **required** for dns mode to work

---

## dns Mode Flags

| Short | Long | Description |
|-------|------|-------------|
| `-d` | `--domain` | Target domain to enumerate |
| `-w` | `--wordlist` | Wordlist to brute force subdomains |
| `-c` | `--show-cname` | Show CNAME records (cannot use with `-i`) |
| `-i` | `--show-ips` | Show IP addresses subdomains resolve to |
| `-r` | `--resolver` | Use a custom DNS server for resolving |

---

## Example
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

**Breakdown:**
- `dns` → subdomain enumeration mode
- `-d example.thm` → target domain
- `-w subdomains-top1million-5000.txt` → wordlist of common subdomains

> Each wordlist entry is used to build a DNS query.
> If entry is `all` → queries `all.example.thm`

---

## Get Help
```bash
gobuster dns --help
```

---

# Gobuster — vhost Mode

## What is vhost Mode?
Brute forces **virtual hosts** — different websites running on the **same server/IP address**.

> Don't confuse with `dns` mode!

| Mode | How it works |
|------|-------------|
| `vhost` | Navigates to URL by combining hostname (`-u`) + wordlist entry |
| `dns` | Does a DNS lookup using domain (`-d`) + wordlist entry |

---

## Basic Syntax
```bash
gobuster vhost -u "http://example.thm" -w /path/to/wordlist
```
> `-u` and `-w` are **required** for vhost mode to work

---

## vhost Mode Flags

| Short | Long | Description |
|-------|------|-------------|
| `-u` | `--url` | Base URL / target domain |
| — | `--append-domain` | Appends base domain to each wordlist entry e.g. `word.example.com` |
| `-m` | `--method` | HTTP method to use e.g. GET, POST |
| — | `--domain` | Appends domain to each wordlist entry to form valid hostname |
| — | `--exclude-length` | Filter out false positives by response body size |
| `-r` | `--follow-redirect` | Follow HTTP redirects (301/302) |

---

## Example
```bash
gobuster vhost -u "http://MACHINE_IP" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250,254
```

**Breakdown:**
- `vhost` → virtual host enumeration mode
- `-u "http://MACHINE_IP"` → target IP/URL
- `--domain example.thm` → sets second + top level domain in `Host:` header
- `-w` → wordlist — each entry tested as a subdomain
- `--append-domain` → appends domain to each entry e.g. `blog` → `blog.example.thm`
- `--exclude-length` → filters false positives by response size

---

## How Gobuster Sends Requests

Gobuster changes the `Host:` header for each request:
```
GET / HTTP/1.1
Host: www.example.thm        ← this changes each request
User-Agent: gobuster/3.6
```

**Host header breakdown:**
```
www        .example     .thm
 ↑              ↑         ↑
subdomain   2nd-level   top-level
(wordlist)  (--domain)  (--domain)
```

---

## Example Output
```
Found: blog.example.thm    Status: 200 [Size: 1493]
Found: shop.example.thm    Status: 200 [Size: 2983]
Found: www.example.thm     Status: 200 [Size: 84352]
Found: academy.example.thm Status: 200 [Size: 434]
```

---

## Important Notes

- Always use `--append-domain` — without it hostname will be just `www`, `blog` etc. causing **false positives**
- Use `--exclude-length` to filter false positives — they usually have similar response sizes
- Status `200` = valid vhost found 
- Status `404` with consistent size = likely false positive 

---

## Get Help
```bash
gobuster vhost --help
```

---
