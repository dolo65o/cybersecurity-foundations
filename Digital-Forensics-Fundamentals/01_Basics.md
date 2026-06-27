# Digital Forensics — Fundamentals

The branch of forensics that investigates cyber crimes is known as digital forensics. Cyber crime is any criminal activity conducted on or using a digital device. Several tools and techniques are used to investigate digital devices thoroughly after any crime to find and analyze evidence for necessary legal action.

## NIST 4-Phase Process

```
Collection → Examination → Analysis → Reporting
```

| Phase | What happens |
|-------|-------------|
| **Collection** | Identify all devices (PCs, USBs, cameras, etc.); gather evidence without tampering; document everything |
| **Examination** | Filter collected data — extract only what's relevant to the case (e.g. specific date/time/user) |
| **Analysis** | Correlate evidence across multiple sources; reconstruct activities chronologically |
| **Reporting** | Prepare detailed report: methodology + findings + recommendations; presented to law enforcement & management; include executive summary |

---

## Types of Digital Forensics

| Type | Focus |
|------|-------|
| **Computer Forensics** | Investigating PCs/laptops — most common type |
| **Mobile Forensics** | Call records, SMS, GPS, app data from mobile devices |
| **Network Forensics** | Network-wide investigation; primary evidence = traffic logs |
| **Database Forensics** | Unauthorized DB access resulting in data modification or exfiltration |
| **Cloud Forensics** | Investigating cloud-stored data; difficult — limited evidence available on cloud infra |
| **Email Forensics** | Investigating emails for phishing or fraud campaigns |

## Evidence Acquisition — Best Practices

### 1. Proper Authorization
- Must obtain authorization from relevant authorities **before** collecting any data
- Evidence collected without approval → **inadmissible in court**
- Required because forensic evidence contains private/sensitive data

---

### 2. Chain of Custody
A formal document that tracks evidence from collection to court. Prevents tampering and proves integrity.

**Required fields:**
- Description of evidence (name, type)
- Name of individual(s) who collected it
- Date and time of collection
- Storage location of each piece
- Access times + who accessed it

> Used to prove **integrity and reliability** of evidence in court.

---

### 3. Write Blockers
- Hardware/software that **blocks any write operations** to the evidence drive
- Problem without it: connecting a suspect's hard drive to a forensic workstation may alter file timestamps via background OS tasks → corrupts evidence
- With write blocker: drive remains in **original unaltered state** throughout acquisition

## Windows Forensics — Image Acquisition & Analysis

### Two Types of Forensic Images

| Type | Storage | Volatile? | Contains |
|------|---------|-----------|----------|
| **Disk Image** | HDD/SSD | No (survives reboot) | Files, documents, browsing history, installed apps |
| **Memory Image** | RAM | Yes (lost on shutdown/restart) | Running processes, open files, active network connections |

> **Critical:** Always take the **memory image first** — RAM data is lost the moment the system is powered off or restarted.

---

### Tools

| Tool | Type | Purpose |
|------|------|---------|
| **FTK Imager** | GUI | Disk image acquisition + basic analysis; supports multiple image formats |
| **Autopsy** | GUI (open-source) | Deep disk image analysis — keyword search, deleted file recovery, file metadata, extension mismatch detection |
| **DumpIt** | CLI | Memory image acquisition from Windows; outputs in multiple formats |
| **Volatility** | CLI (open-source) | Memory image analysis; plugin-based — one plugin per artifact type; supports Windows, Linux, macOS, Android |

---

## Document & Image Metadata Forensics

### Case Setup
```bash
cd /root/Rooms/introdigitalforensics
```

---

### PDF Metadata — `pdfinfo`

**Usage:**
```bash
pdfinfo DOCUMENT.pdf
```

**Example output (DOCUMENT.pdf):**
```
Creator:      Microsoft® Word for Office 365
Producer:     Microsoft® Word for Office 365
CreationDate: Wed Oct 10 21:47:53 2018 EEST
ModDate:      Wed Oct 10 21:47:53 2018 EEST
Pages:        20
Page size:    595.32 x 841.92 pts (A4)
File size:    560362 bytes
PDF version:  1.7
```
> Reveals: software used to create the doc, creation date/time, page count — useful for attribution

---

### Image EXIF Data — `exiftool`

**EXIF** = Exchangeable Image File Format — metadata embedded in image files by cameras/smartphones.

**Common EXIF fields:**
- Camera / smartphone model
- Date and time of capture
- Focal length, aperture, shutter speed, ISO
- **GPS coordinates** (if taken on a GPS-enabled device)


**Usage:**
```bash
exiftool IMAGE.jpg
```

**Example output:**
```
GPS Position : 51 deg 31' 4.00" N, 0 deg 5' 48.30" W
```

**Convert GPS for map search:**
- Replace `deg` with `°` and remove extra spaces
- Search format: `51°30'51.9"N 0°05'38.7"W` in Google Maps / Bing Maps
- → Reveals the physical location where the photo was taken
