# CyberChef — Data Analysis Tool

## What is CyberChef?
A web-based "Swiss Army knife" for data operations — encoding, decoding, encryption, decryption, and more.
Operates on **recipes** — a series of operations executed in sequence.

**Common operations:**
- Encoding: XOR, Base64
- Encryption/Decryption: AES, RSA
- And many more

---

## Access Methods

| Method | How |
|--------|-----|
| **Online** | https://gchq.github.io/CyberChef (browser + internet required) |
| **Offline/Local** | Download latest stable release from https://github.com/gchq/CyberChef/releases — works on Windows & Linux |

> Best practice: Download the most stable release, not the latest bleeding-edge version.

---
## CyberChef — Interface & Operations

### Four Areas

<img width="2984" height="1660" alt="1" src="https://github.com/user-attachments/assets/bc581fbd-85a5-4c3f-9555-439bd4ce561c" />

---

### Common Operations

| Operation | What it does | Example |
|-----------|-------------|---------|
| **From Morse Code** | Morse → alphanumeric | `- .... .-. . .- - ...` → `THREATS` |
| **URL Encode** | Encodes special chars to percent-encoding | `https://tryhackme.com` → `https%3A%2F%2Ftryhackme%2Ecom` |
| **To Base64** | Raw data → Base64 ASCII string | `This is fun!` → `VGhpcyBpcyBmdW4h` |
| **To Hex** | String → hex bytes | `This` → `54 68 69 73` |
| **To Decimal** | String → ordinal integers | `This` → `84 104 105 115` |
| **ROT13** | Caesar cipher (default: rotate 13) | `Digital Forensics` → `Qvtvgny Sberafvpf` |

> Hover over any operation to see a sample, description, and Wikipedia link.

---

### Recipe Area (the heart of CyberChef)
- Drag operations here and set their arguments
- **Save recipe** — save current op set for reuse
- **Load recipe** — reload a saved recipe
- **Clear recipe** — wipe current ops
- **BAKE!** — process input with current recipe
- **Auto Bake** — processes automatically on any change (no manual BAKE needed)

---

### Input Area Features
| Feature | Purpose |
|---------|---------|
| Add new input tab | Use multiple different inputs simultaneously |
| Open file as input | Upload a file directly |
| Open folder as input | Upload entire folder |
| Clear input and output | Reset everything |
| Reset pane layout | Restore default window sizes |

<img width="1698" height="944" alt="input area" src="https://github.com/user-attachments/assets/eb80787b-df46-435c-ad60-923a7ac16a46" />

---

### Output Area Features
| Feature | Purpose |
|---------|---------|
| Save output to file | Saves result as `.dat` file |
| Copy raw output | Copies result to clipboard |
| Replace input with output | Overwrites input with current output (chain operations) |
| Maximise output pane | Expand output view |

<img width="1530" height="766" alt="output area" src="https://github.com/user-attachments/assets/dfbd7984-9b0f-41db-b629-33c343829595" />

---

## CyberChef — Workflow

### 4-Step Process

```
1. Set Objective → 2. Input Data → 3. Select Operations → 4. Check Output
        ↑___________________________|  (repeat if needed)
```

---

### Step-by-Step

**1. Set a Clear Objective**
Define exactly what you want to achieve.
> Example: "I found a gibberish string during a security investigation — I want to decode it."

**2. Input Your Data**
Paste, type, or upload the data into the Input area.

**3. Select Operations**
Pick operations based on what you suspect the encoding/encryption might be.
If unsure → try common ones systematically:

| Try first | Why |
|-----------|-----|
| `From Base64` | Most common encoding |
| `ROT13` / `ROT47` | Simple substitution ciphers |
| `From Base85` | Less common but used |
| `From Hex` | If input looks like hex bytes |

**4. Check Output**
Does it make sense? Is it readable?
- **Yes** → objective achieved
- **No** → swap/add operations and repeat

---

## CyberChef — Key Operation Categories

### Extractors

| Operation | What it extracts |
|-----------|-----------------|
| **Extract IP addresses** | All valid IPv4 and IPv6 addresses |
| **Extract URLs** | URLs from input (protocol required — HTTP, FTP, etc.) |
| **Extract email addresses** | Strings matching `anything@domain.com` format |

> URL extractor requires protocol prefix — without it you get too many false positives.

---

### Date & Time

| Operation | Purpose | Example |
|-----------|---------|---------|
| **To UNIX Timestamp** | Datetime string → seconds since Jan 1 1970 UTC | `Fri Sep 6 20:30:22 +04 2024` → `1725654622` |
| **From UNIX Timestamp** | UNIX timestamp → readable datetime string | `1725654622` → `Fri Sep 6 20:30:22 2024` |

---

### Data Format — Base Encodings

| Operation | Example |
|-----------|---------|
| **From Base64** | `V2VsY29tZSB0byB0cnloYWNrbWUh` → `Welcome to tryhackme!` |
| **From Base85** | `BOu!rD]j7BEbo7` → `hello world` |
| **From Base58** | `AXLU7qR` → `Thm58` |
| **To Base62** | `Thm62` → `6NiRkOY` |
| **URL Decode** | `https%3A%2F%2Fgchq%2Egithub%2Eio` → `https://gchq.github.io` |

**Base encoding** = converts binary data into ASCII text using a defined character set.

---

### How Base64 Works (Manual Walkthrough)
Encoding `THM`:

**Step 1 — ASCII → Binary, concatenate:**
```
T = 01010100
H = 01001000
M = 01001101
→  010101000100100001001101  (24 bits)
```

**Step 2 — Split into 6-bit chunks → Decimal:**
```
010101 → 21
000100 →  4
100001 → 33
001101 → 13
```

**Step 3 — Map to Base64 index table:**
```
21 → V
 4 → E
33 → h
13 → N
→ THM = VEhN
```

---

### Common URL Percent-Encoding Reference

| Character | UTF-8 Encoded |
|-----------|--------------|
| `:` | `%3A` |
| `/` | `%2F` |
| `.` | `%2E` |
| `=` | `%3D` |
| `#` | `%23` |
