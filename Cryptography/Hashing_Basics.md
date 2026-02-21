# Hashing Basics

Hashing is a fundamental cryptographic concept used to maintain data integrity and secure passwords. 

## 1. What is a Hash Function?
Hash functions operate differently than standard encryption because they lack a key and are designed to be practically impossible to reverse. 

* **The Digest:** The algorithm takes input data of any arbitrary size and condenses it into a fixed-size summary, commonly referred to as a digest.
* **The Avalanche Effect:** A robust hashing algorithm ensures that even the slightest alteration to the input data—such as changing a single bit—will result in a drastically different output. 
* **Encoding:** The raw byte output of a hash function is typically encoded into a more readable format, such as base64 or hexadecimal.


## 2. Practical Application and Commands
To observe how sensitive hash functions are to input changes, you can compare two nearly identical files. For instance, a file containing the letter 'T' (hexadecimal 54) and one containing 'U' (hexadecimal 55) differ by just one bit.

You can generate and view these hashes using built-in Linux commands. Here is how you calculate the hash for multiple text files in a directory:

**Calculating MD5 Hashes:**
```
md5sum *.txt
```

Output:
```
b9ece18c950afbfa6b0fdbfa4ff731d3  file1.txt
4c614360da93c0a041b22e537de151eb  file2.txt
```
Running standard Linux commands reveals that their resulting hashes share no resemblance:
* `md5sum *.txt` calculates the MD5 hash.
* `sha1sum *.txt` calculates the SHA1 hash.
* `sha256sum *.txt` calculates the SHA-256 hash.

## 3. The Importance of Hashing
You interact with hashing constantly behind the scenes, primarily during authentication. 

Instead of storing your plaintext password, secure servers record the hash value of that password. When you attempt to log in, the system calculates the hash of your submitted attempt and verifies if it matches the stored digest. 

## 4. Hash Collisions and Insecure Algorithms
A hash collision happens when two completely distinct inputs generate the exact same output. 

* **The Pigeonhole Effect:** Because hash functions accept a practically unlimited number of inputs but only produce a limited number of fixed-size outputs, collisions are mathematically inevitable. If you have more items than containers, some containers must hold multiple items.


* **Deprecated Standards:** Algorithms like MD5 and SHA1 have been successfully attacked by researchers who figured out how to intentionally engineer these collisions. Consequently, neither MD5 nor SHA1 should be trusted for hashing sensitive data or passwords today.

---

# Insecure Password Storage for Authentication

Hashing is widely used in cybersecurity for password storage and data integrity. While password managers require the ability to retrieve passwords in cleartext, authentication mechanisms only need to confirm that the user knows the password to grant access.

Storing passwords securely is critical because users frequently reuse passwords across multiple services; a leak from one database can jeopardize a user's other accounts, such as their online banking.

There are three major insecure practices regarding password storage:

## 1. Storing Passwords in Plaintext
Storing passwords without any form of encryption or hashing is a severe security flaw. 

* **The RockYou Breach:** A company named RockYou, which developed social media applications and widgets, stored user passwords in plaintext. 
* **The Aftermath:** This led to a massive data breach exposing over 14 million passwords. 
* **The Wordlist:** This leaked list, named `rockyou.txt`, is now commonly included in offensive security distributions like Kali Linux within the `/usr/share/wordlists` directory.

**Example from Terminal:**
```bash
strategos@g5000 /usr/share/wordlists> wc -l rockyou.txt
14344392 rockyou.txt

strategos@g5000 /usr/share/wordlists> head rockyou.txt
123456
12345
123456789
password
iloveyou
princess
1234567
rockyou
12345678
abc123
```
## 2. Using an Insecure Encryption Algorithm
Instead of using secure hashing functions, some companies have mistakenly used deprecated encryption formats.
  - **The Adobe Breach**: Adobe suffered a notable breach where they used a deprecated encryption format to store passwords.
  - **The Flaw**: Furthermore, password hints were stored in plain text alongside them, and these hints sometimes contained the password itself. This allowed attackers to retrieve the plaintext passwords relatively quickly.

## 3. Using an Insecure Hash Function
Even when hashing is utilized, using an outdated algorithm or failing to implement proper techniques leaves data vulnerable.
  - **The LinkedIn Breach**: In 2012, LinkedIn experienced a data breach due to using SHA-1, an insecure hashing algorithm, to store user passwords.
  - **Missing Security Controls**: Additionally, LinkedIn did not use password salting.
  - **What is Salting?** Password salting is the practice of adding a "salt"—a random value—to the password before it is hashed to provide extra security.

---

# Secure Password Storage: Salting & Rainbow Tables

While using a hash function is infinitely better than storing passwords in plaintext, basic hashing alone is no longer sufficient to protect user credentials. 

## 1. The Flaw with Basic Hashing
The primary weakness of basic hashing is that a hash function will always produce the exact same output for the same input. 

* **The Duplicate Problem:** If two different users happen to choose the exact same password, their stored hash values will be identical. 
* **The Risk:** If an attacker manages to crack one hash, they instantly gain access to every other account sharing that same password. Furthermore, this predictability allows for the use of pre-computed attacks like Rainbow Tables.

## 2. Rainbow Tables
A **Rainbow Table** is a massive lookup table that maps pre-computed hash values back to their original plaintext passwords. 

* **Time vs. Space:** Creating a rainbow table takes significant computational time, but once generated, it trades that cracking time for hard disk space. 
* **The Threat:** Searching through a sorted list of hashes is dramatically faster than trying to compute and crack a hash dynamically. Services like CrackStation and Hashes.com leverage massive rainbow tables to provide near-instant password cracking for *unsalted* hashes.


## 3. Defeating Rainbow Tables with "Salting"
To mitigate the threat of rainbow tables, security systems use a technique called "salting". 

* **What is a Salt?** A salt is a randomly generated string of characters that is added to the user's password *before* it gets hashed. 
* **The Mechanism:** The salt must be unique to each individual user. Because the salt is unique, even if two users have the exact same plaintext password, their final combined hashes will look completely different. 
* **Storage:** Salts do not need to be kept secret; they are safely stored in the database right next to the hash value. Modern hashing functions like Bcrypt and Scrypt handle this salting process automatically.

## 4. Best Practices Example: Secure Storage Workflow
When properly securing user passwords from scratch, follow these exact steps:

1. **Select Algorithm:** Choose a modern, secure hashing function designed for passwords (e.g., Argon2, Scrypt, Bcrypt, or PBKDF2).
2. **Generate Salt:** Create a unique, random salt for the specific user (e.g., `Y4UV*^(=go_!`).
3. **Concatenate:** Combine the plaintext password with the unique salt. For a password of `AL4RMc10k`, the combined string becomes `AL4RMc10kY4UV*^(=go_!`.
4. **Hash:** Calculate the hash value of this newly combined string using the selected algorithm.
5. **Store:** Save both the final hash value and the unique salt used (`Y4UV*^(=go_!`) in the database.

## 5. Why Not Just Encrypt the Passwords?
It might seem simpler to just use symmetric encryption to protect passwords, but this introduces a critical vulnerability: Key Management. 

If you encrypt the database, you must store the decryption key somewhere. If an attacker breaches your systems and locates that single key, they can instantly decrypt and steal every single user password in your database. Hashing remains one-way, neutralizing this risk.

---

# Hash Recognition for Offensive Security

Transitioning from defensive strategies to offensive security requires the ability to recognize hash types before attempting to crack them and recover the original passwords.

While automated recognition tools like `hashID` exist, they can be unreliable for certain formats. For example, these tools often mix up MD5 and NTLM hashes. Therefore, relying on environmental context is essential; discovering a hash within a web application database makes it far more likely to be MD5 than NTLM.

## 1. Linux Password Hashes
Modern Linux operating systems store password hashes in the `/etc/shadow` file, which is typically restricted to root access. Historically, passwords resided in `/etc/passwd`, exposing them to any user on the system. 

The `shadow` file structures its data across nine fields delimited by colons (`:`). The second field contains the encrypted passphrase, formatted predictably as `$prefix$options$salt$hash`. The prefix is the crucial identifier for the hashing algorithm utilized.


### Common Unix-Style Prefixes
The following table outlines standard prefixes found in Linux systems, ordered from strongest to weakest:

| Prefix | Algorithm | Description |
| :--- | :--- | :--- |
| `$y$` | **yescrypt** | A scalable hashing scheme; the default and recommended choice for new systems. |
| `$gy$` | **gost-yescrypt** | Utilizes the GOST R 34.11-2012 hash function alongside the yescrypt method. |
| `$7$` | **scrypt** | A password-based key derivation function. |
| `$2b$`, `$2y$`, `$2a$`, `$2x$` | **bcrypt** | Based on the Blowfish block cipher, originally developed for OpenBSD and supported across many modern Unix-like systems. |
| `$6$` | **sha512crypt** | Based on SHA-2 with a 512-bit output, commonly found on older Linux systems. |
| `$md5` | **SunMD5** | Based on the MD5 algorithm, originally developed for Solaris. |
| `$1$` | **md5crypt** | Based on the MD5 algorithm, originally developed for FreeBSD. |

### Practical Example Breakdown
Consider this terminal output querying the shadow file for a specific user:

```bash
root@TryHackMe# sudo cat /etc/shadow | grep strategos
strategos:$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4:19965:0:99999:7:::
```
- Focusing on the components separated by the `$` symbol:
    - `y`: Indicates the hash algorithm is yescrypt.
    - `j9T`: Represents the parameters passed to the algorithm.
    - `76UzfgEM5PnymhQ7TlJey1`: The unique salt applied to the password.
    - `/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4`: The final computed hash value.

## 2. Windows Password Hashes
Microsoft Windows manages authentication differently, relying on NTLM (a variant of MD4) for password hashing.
  - **Storage location**: These credentials reside within the SAM (Security Accounts Manager) database.
  - **Extraction**: While the operating system actively prevents standard users from accessing this database, specialized tools like **mimikatz** are designed to bypass these protections and dump the hashes.
  - **Identification**: Visually, an NTLM hash looks identical to MD4 and MD5 hashes, reinforcing the need to use environmental context for accurate identification.

---

# Cracking Password Hashes

When passwords are salted, pre-computed rainbow tables are no longer effective. Because you cannot "decrypt" a hash, you must attempt to crack it by hashing numerous different inputs and comparing the results to the target hash.

Industry-standard tools for this process include **[Hashcat](https://hashcat.net/hashcat/)** and **[John the Ripper](https://www.openwall.com/john/)**. They automate the process of taking a massive list of potential passwords (like `rockyou.txt`), applying the known hash algorithm (and salt, if applicable), and looking for a match.

## 1. Hardware Considerations: GPUs vs. VMs

The speed at which you can crack a hash depends heavily on your hardware and the hashing algorithm used.

* **The Power of GPUs:** Modern Graphics Processing Units (GPUs) contain thousands of cores. While they cannot execute standard CPU tasks, they are highly specialized for the mathematical calculations involved in most hash functions, allowing you to crack many hash types exceptionally quickly. 
* **Algorithm Resistance:** Some modern hashing algorithms, such as Bcrypt, are intentionally designed to resist GPU acceleration, meaning hashing on a GPU provides no speed improvement over a CPU.
* **The Virtual Machine Limitation:** Cracking hashes inside a Virtual Machine (VM) is generally inefficient. VMs typically do not have direct access to the host machine's graphics card, and virtualization introduces overhead that degrades CPU performance. 
* **Best Practice:** For optimal performance, run Hashcat directly on your host operating system (Windows builds are available) to fully leverage your GPU hardware. John the Ripper relies on the CPU by default, but it will still perform better on the host OS without virtualization overhead.

## 2. Using Hashcat

Hashcat is a powerful, command-line-driven advanced password recovery utility. 

### Basic Syntax
The fundamental structure of a Hashcat command is as follows:

```bash
hashcat -m <hash_type> -a <attack_mode> hashfile wordlist
```
### Flag Breakdown
- `-m <hash_type>`: Specifies the exact algorithm used to generate the hash, represented by a numeric code. For example, `-m 1000` tells Hashcat to treat the target as an NTLM hash. You must consult the Hashcat documentation or example page to find the correct code for your target hash.
- `-a <attack_mode>`: Specifies how Hashcat should attempt to crack the password. For a standard dictionary attack (trying passwords straight from a list one after another), you use `-a 0`.
- `hashfile`: The path to the text file containing the hash(es) you are trying to crack.
- `wordlist`: The path to the dictionary file you want to use, such as the `rockyou.txt` file.

### Practical Command Example
If you want to crack a Bcrypt hash stored in hash.txt using the rockyou.txt wordlist via a straight dictionary attack, you would execute the following command:`hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt`

---

# Data Integrity and HMACs

Beyond storing passwords securely, hash functions serve a critical role in verifying the integrity of data.

## 1. Integrity Checking
Hashing provides a reliable method to confirm that files remain unchanged. Because hash functions deterministically produce the same output for the exact same input, any modification to a file—even a single bit—will drastically alter its resulting hash.

* **File Verification:** When downloading software, such as operating system ISOs, developers often provide the official hash value alongside the download link. You can compute the hash of your local copy using utilities like `sha256sum` and compare it against the official record to guarantee your file is authentic and uncorrupted.
* **Duplicate Detection:** Since identical documents generate the exact same hash, computing hashes is a highly efficient technique for identifying and removing duplicate files across a system.

## 2. HMAC (Keyed-Hash Message Authentication Code)
Standard hashing proves that a file has not changed, but it does not prove the identity of the person who created the file or hash. An HMAC addresses this limitation by combining a cryptographic hash function with a secret key.

* **Authenticity and Integrity:** By incorporating a secret key, an HMAC verifies both the identity of the creator (authenticity) and that the data remains intact (integrity).

### The HMAC Process
Generating an HMAC involves a specific sequence of cryptographic operations:

1. The secret key is padded to match the block size of the chosen hash function.
2. This padded key is then XORed with a constant value, typically a block of zeros or ones.
3. The actual message is hashed using the hash function alongside the XORed key from the previous step.
4. The result of that first hash is hashed a second time, utilizing the padded key XORed with a different constant.
5. This final operation yields the fixed-size HMAC string.

# HMAC Process

Assume:
- Secret Key = K
- Message = M
- Hash Function = H

## Step 1: Key Padding

If the key is shorter than the hash block size → pad with zeros  
If longer → hash it first

## Step 2: Inner Key Mixing

Compute: `K ⊕ ipad`

Where:
- `ipad` = Inner padding constant

## Step 3: Inner Hash

Hash the combined value: `InnerHash = H((K ⊕ ipad) || M)`

## Step 4: Outer Key Mixing

Compute: `K ⊕ opad`

Where:
- `opad` = Outer padding constant

## Step 5: Final HMAC

Hash again: `HMAC = H((K ⊕ opad) || InnerHash)`

## Final Formula

$HMAC(K, M) = H((K \oplus opad) || H((K \oplus ipad) || M))$

   <img width="598" height="654" alt="HMAC" src="https://github.com/user-attachments/assets/ed4b314e-ce2f-42f2-9f73-a998e5f1bd3d" />


* $M$ represents the message being authenticated.
* $K$ represents the secret key.
* $H$ denotes the cryptographic hash function.
* $\oplus$ indicates the XOR operation.
* $ipad$ and $opad$ are the inner and outer padding constants.
