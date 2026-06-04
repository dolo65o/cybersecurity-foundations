# Hydra — Introduction

## What is Hydra?
A **brute force online password cracking tool** that automates
guessing passwords across many authentication services.

> Instead of manually guessing passwords, Hydra runs through a **wordlist** and tests each one automatically at speed.

---

## Supported Protocols
Hydra can brute force a huge range of services including:

| Category | Protocols |
|----------|-----------|
| **Remote Access** | SSH (v1&v2), RDP, Telnet, VNC |
| **Web** | HTTP-GET, HTTP-POST, HTTPS, HTTP-FORM-GET, HTTP-FORM-POST |
| **File Transfer** | FTP, SFTP |
| **Email** | SMTP, IMAP, POP3 |
| **Database** | MySQL, MSSQL, MongoDB, PostgreSQL, Oracle |
| **Network** | SMB, LDAP, SNMP, SOCKS5, RTSP |

> Full list: Asterisk, AFP, Cisco AAA, CVS, Firebird, ICQ, IRC, MEMCACHED, NCP, NNTP, Radmin, Rexec, SAP/R3, SIP, SSHKEY, Subversion, TeamSpeak, VMware-Auth, XMPP...

---

## Why Strong Passwords Matter

> If your password is:
> - Common (in a wordlist)
> - No special characters
> - Under 8 characters
> **Hydra will crack it.**

- Password lists contain **100 million+** common passwords
- Default credentials like `admin:password` are tried first CCTV cameras, routers, and web frameworks often ship with default credentials — **always change them!**

---

# Hydra — Commands & Usage

## Common Options

| Option | Description |
|--------|-------------|
| `-l` | Specify username |
| `-P` | Specify password wordlist |
| `-t` | Number of threads to run in parallel |
| `-V` | Verbose — show every attempt |
| `-s` | Specify non-default port |

---

## FTP Brute Force
```bash
hydra -l user -P passlist.txt ftp://MACHINE_IP
```

---

## SSH Brute Force
```bash
hydra -l <username> -P <full path to pass> MACHINE_IP -t 4 ssh
```

**Example:**
```bash
hydra -l root -P passwords.txt MACHINE_IP -t 4 ssh
```
- Uses `root` as username
- Tries every password in `passwords.txt`
- Runs **4 threads** in parallel (`-t 4`)

---

## Web Form (POST) Brute Force

### Syntax
```bash
sudo hydra -l <username> -P <wordlist> MACHINE_IP http-post-form
"<path>:<login_credentials>:<invalid_response>"
```

### Options Breakdown

| Option | Description | Example |
|--------|-------------|---------|
| `-l` | Username | `admin` |
| `-P` | Password wordlist | `rockyou.txt` |
| `http-post-form` | Form type is POST | — |
| `<path>` | Login page URL | `login.php` or `/` |
| `<login_credentials>` | Form field names | `username=^USER^&password=^PASS^` |
| `<invalid_response>` | Text shown on failed login | `incorrect` |
| `-V` | Show every attempt | — |

### Example
```bash
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form
"/:username=^USER^&password=^PASS^:F=incorrect" -V
```

**Breakdown:**
- `/` = login page is at root (main IP)
- `username` = form field name for username
- `^USER^` = replaced by your `-l` value
- `password` = form field name for password
- `^PASS^` = replaced by each password from wordlist
- `F=incorrect` = string that appears when login **fails**

---

## Custom Port Example
```bash
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form
"/:username=^USER^&password=^PASS^:F=incorrect" -s <port> -V
```
> Use `-s <port>` when web server runs on non-default port

---
