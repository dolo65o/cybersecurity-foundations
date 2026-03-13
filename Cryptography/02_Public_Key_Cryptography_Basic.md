# Cryptography: The Hybrid Model Analogy 

Understanding how Symmetric and Asymmetric encryption work together can be difficult. A physical analogy helps explain why we often use both systems in a single connection.

---

## 1. The "Locked Box" Analogy 
Imagine you want to send secret instructions to a friend, but you don't want anyone else to read them while they are being delivered.

* **The Problem:** You have a secret code (Symmetric Key) that you want to use for future chats, but you can't just yell it across the room (Network) because eavesdroppers will hear it.
* **The Solution:**
    1.  You ask your friend for a **Lock** (Public Key) that only they have the key to.
    2.  You put your secret instructions inside an indestructible box and lock it with their lock.
    3.  You send the locked box to your friend.
    4.  Your friend uses their **Key** (Private Key) to unlock the box and retrieve the instructions.
    5.  Now, both of you know the secret instructions and can communicate privately using that code.

### Concept Mapping Table 

| Physical Analogy | Cryptographic Component |
| :--- | :--- |
| **Secret Code** | Symmetric Encryption Cipher & Key |
| **Lock** | Public Key (Shared with everyone) |
| **Lock's Key** | Private Key (Kept secret by recipient) |

## 2. Why do we do this? 
This hybrid approach gives us the best of both worlds:
* **Security:** We use **Asymmetric Encryption** (The Lock/Private Key) just once to securely share the secret key.
* **Speed:** Once the secret key is shared, we switch to **Symmetric Encryption** (The Secret Code) for the rest of the conversation because it is much faster.

## 3. The Real World: Identity Verification 
Encryption protects the *content* of the message, but how do you know who sent it?
* In the real world, you need to verify that the person you are talking to is actually who they claim to be.
* This is achieved using **Digital Signatures** and **Certificates**, which validate the identity of the sender.

---

# RSA Encryption: The Math of Security 

**RSA** (Rivest–Shamir–Adleman) is a public-key encryption algorithm that enables secure data transmission over insecure channels. Its security is fundamentally based on a mathematical asymmetry: while it is easy to multiply numbers, it is incredibly difficult to factor them back apart.

## 1. The Mathematical Foundation 

RSA relies on the difficulty of **factoring large prime numbers**.

* **The Easy Direction (Multiplication):** Multiplying two large prime numbers is computationally trivial.
    * *Example:* $113 \times 127 = 14351$.
    * Even with massive numbers (e.g., 300 digits), a computer can do this instantly.
* **The Hard Direction (Factorization):** Taking a massive product and finding the original two prime factors is practically infeasible for modern computers.
* **Scale:** A computer cannot currently factor a number with more than **600 digits** in a reasonable timeframe.


## 2. How RSA Works (Step-by-Step) 

The algorithm uses modular arithmetic to generate a public and private key pair.

### A. Key Generation
1.  **Select Primes:** Choose two distinct prime numbers, $p$ and $q$.
    * *Example:* $p = 157$, $q = 199$.
2.  **Calculate Modulus ($n$):**
    $$n = p \times q = 31243$$
3.  **Calculate Totient ( $\phi(n)$ ):**
    $\phi(n) = (p-1)(q-1) = 156 \times 198 = 30888$
4.  **Choose Public Exponent ($e$):** Select an $e$ that is relatively prime to $\phi(n)$.
    * *Example:* $e = 163$.
    * **Public Key:** $(n, e) \rightarrow (31243, 163)$.
5.  **Calculate Private Exponent ($d$):** Find $d$ such that $(e \times d) \pmod{\phi(n)} = 1$.
    * *Example:* $d = 379$ (since $163 \times 379 = 61777$, and $61777 \pmod{30888} = 1$).
    * **Private Key:** $(n, d) \rightarrow (31243, 379)$.

### B. Encryption & Decryption
* **Encryption (Alice):** To send a message $x = 13$:
    $$y = x^e \pmod n$$
    $$16341 = 13^{163} \pmod{31243}$$
* **Decryption (Bob):** To recover the message $y = 16341$:
    $$x = y^d \pmod n$$
    $$13 = 16341^{379} \pmod{31243}$$


## 3. RSA in CTFs (Capture The Flag) 

In security competitions (CTFs), RSA challenges often require you to break weak encryption by calculating the missing variables.

### Key Variables Cheat Sheet
| Variable | Description | Formula/Notes |
| :--- | :--- | :--- |
| **$p, q$** | Large Prime Numbers | Kept secret (used to make $n$) |
| **$n$** | Modulus | $n = p \times q$ (Public) |
| **$e$** | Public Exponent | Part of the **Public Key** |
| **$d$** | Private Exponent | Part of the **Private Key** |
| **$c$** | Ciphertext | The encrypted message |
| **$m$** | Plaintext | The original message |

### Recommended Tools 
* **RsaCtfTool**: Automates attacks on weak RSA keys.
* **rsatool**: Another utility for calculating RSA parameters.

---

# Diffie-Hellman Key Exchange 

**Diffie-Hellman** is a method that allows two parties to securely establish a shared secret over an insecure communication channel.

* **Goal:** To create a shared "secret key" without ever sending that key across the network.
* **Usage:** This shared secret is then used to encrypt subsequent communications using faster **Symmetric Encryption**.


## 1. The Concept 

Imagine Alice and Bob want to agree on a secret color (the key) without anyone else finding out, but they can only shout messages across a crowded room.

1.  **Private Secrets:** Alice and Bob each generate their own random secret.
2.  **Public Material:** They agree on some common public material.
3.  **Mixing:** They combine their private secret with the public material and send the result to each other.
4.  **Final Combination:** They take the result they received and combine it *again* with their private secret.

> **Result:** Because the order of combination doesn't matter, they both end up with the exact same final value (the Shared Secret).


## 2. The Algorithm (Step-by-Step) 

The mathematical process relies on modular arithmetic to ensure the secrets cannot be reverse-engineered easily.

### Step 1: Agree on Public Variables
Alice and Bob agree on two public numbers that anyone can see:
* **$p$**: A large prime number (e.g., $29$).
* **$g$**: A generator ($0 < g < p$) (e.g., $3$).

### Step 2: Choose Private Keys
Each party picks a secret number that **never** leaves their device.
* **Alice's Private Key ($a$):** $13$.
* **Bob's Private Key ($b$):** $15$.

### Step 3: Calculate Public Keys
They calculate a value to send to the other person.
* **Alice calculates ($A$):**
    $$A = g^a \pmod p$$
    $$A = 3^{13} \pmod{29} = 19$$
* **Bob calculates ($B$):**
    $$B = g^b \pmod p$$
    $$B = 3^{15} \pmod{29} = 26$$

### Step 4: Key Exchange 
* Alice sends **19** to Bob.
* Bob sends **26** to Alice.
* *An attacker watching the network only sees 29, 3, 19, and 26.*

### Step 5: Calculate Shared Secret
They use the number they received to calculate the final secret.
* **Alice (uses Bob's public $B$):**
    $$Secret = B^a \pmod p$$
    $$Secret = 26^{13} \pmod{29} = 10$$
* **Bob (uses Alice's public $A$):**
    $$Secret = A^b \pmod p$$
    $$Secret = 19^{15} \pmod{29} = 10$$

**Conclusion:** Both Alice and Bob now have the shared secret **10**, which they can use to encrypt their messages.

---

# SSH Authentication Essentials 

Secure Shell (SSH) is not just about logging in; it involves a two-way verification process to ensure both the server and the client are who they claim to be.

## 1. Authenticating the Server 
When you connect to an SSH server for the first time, your client does not know if it is talking to the real server or an imposter (Man-in-the-Middle).

* **The Warning:** You will see a message saying "The authenticity of host... can't be established" followed by a key **fingerprint**.
* **The Check:** You must verify this fingerprint (a unique identifier derived from the server's public key) against a trusted source.
* **The Decision:**
    * If you type `yes`, the client trusts the server and saves its public key signature locally.
    * Future connections will be silent unless the server's key changes (which could indicate an attack).


## 2. Authenticating the Client (SSH Keys) 
While passwords are common, **Public Key Authentication** is the preferred method for security. It uses a pair of cryptographic keys instead of a password.

* **Public Key:** Shared with the server (like a lock).
* **Private Key:** Kept secret on your machine (like the key to that lock).

### Generating Keys (`ssh-keygen`)
The tool `ssh-keygen` creates these key pairs. It supports several algorithms:
* **RSA:** The old standard. Keys are very long.
* **Ed25519:** A modern, high-performance algorithm. Keys are much shorter and secure.

**Command Example:**
``ssh-keygen -t ed25519``

> Passphrase: You can add a passphrase to encrypt the private key on your disk. This passphrase is never sent to the server; it only unlocks the key locally.

## 3. Key Management & Permissions

### File Structure
  * When you generate keys (e.g., Ed25519), two files are created in your `~/.ssh/ directory`:
    * id_ed25519: The Private Key. Never share this.
    * id_ed25519.pub: The Public Key. This is safe to share.

### Installation & Permissions
  * Server Side: The Public Key content must be added to the `~/.ssh/authorized_keys` file on the remote server.
  * Client Side: The Private Key file must have strict permissions (600), meaning only the owner can read/write it.
    
> Command: ``chmod 600 id_ed25519``
> If permissions are too open, the SSH client will ignore the key for security reasons.
> To connect using a specific private key: `ssh -i privateKeyFileName user@host`

## 5. CTF Strategy: The "Better Shell"

In Capture The Flag (CTF) challenges, you often start with a "reverse shell," which is unstable (it crashes if you press Ctrl+C and lacks tab completion).
  * The Upgrade: If you can write to the target's file system, you can inject your own Public Key into their `~/.ssh/authorized_keys` file.
  * The Result: You can then SSH into the machine normally, giving you a fully stable shell with all features.

---

# Digital Signatures & Certificates 

In the digital world, we cannot rely on physical signatures, stamps, or fingerprints to prove identity. instead, we use **Digital Signatures** to verify the authenticity and integrity of a message or document.

---

## 1. What is a Digital Signature? 

A digital signature is a cryptographic method used to prove two things:
1.  **Authenticity:** Confirming who created or signed the file.
2.  **Integrity:** Confirming the file has not been modified since it was signed.

### How It Works (The Asymmetric Reversal)
We normally use Public Keys to encrypt and Private Keys to decrypt. Digital signatures reverse this logic:
* **Signing:** You create a signature using your **Private Key** (which only you possess).
* **Verifying:** Anyone can use your **Public Key** to verify that the signature was made by your Private Key.

### Electronic vs. Digital Signatures
* **Electronic Signature:** Often refers to simply pasting an image of a signature onto a document. This is insecure as anyone can copy-paste an image.
* **Digital Signature:** A cryptographic process where the sender encrypts a **hash** of the document. The recipient decrypts this hash and compares it to the actual file to ensure it matches exactly.

---

## 2. Certificates: Proving Who You Are 

While signatures prove *integrity*, how do you know the Public Key actually belongs to the person/company they claim to be? This is where **Certificates** come in.

### The Chain of Trust 
Certificates rely on a hierarchy of trust to validate identities, particularly for web browsing (HTTPS).

1.  **Root CA (Certificate Authority):** These are trusted organizations (e.g., DigiCert, Let's Encrypt). Your operating system and browser come pre-installed with a list of Root CAs they automatically trust.
2.  **Intermediate CA:** The Root CA signs certificates for organizations, vouching for them.
3.  **End-Entity Certificate:** This is the certificate you see on a website (e.g., `tryhackme.com`).

> *Logic:* Your browser trusts the Root CA -> The Root CA trusts the Organization -> Therefore, your browser trusts the Organization's website.

### TLS Certificates & HTTPS 
To use HTTPS, a website must have a **TLS Certificate**.
* **Paid:** You can buy them from various authorities for an annual fee.
* **Free:** Organizations like **[Let's Encrypt](https://letsencrypt.org/)** provide free TLS certificates to encourage a more secure web.

---

# PGP & GPG Essentials 

**PGP** (Pretty Good Privacy) is a software suite used for encrypting files, performing digital signing, and protecting data confidentiality.

**GPG** (GNU Privacy Guard), also known as **GnuPG**, is the open-source implementation of the OpenPGP standard.

## 1. Core Use Cases 

GPG is commonly used to secure communications, particularly emails:
* **Confidentiality:** Encrypting email messages so only the recipient can read them.
* **Integrity:** Signing an email message to confirm it hasn't been altered and verifying the sender's identity.

## 2. Generating Keys 

To start using GPG, you must generate a key pair (Public and Private).

**Command:**
`gpg --full-gen-key`

### The Interactive Process:

    * Select Algorithm: You will be asked to choose the key type. The modern default is often (9) ECC (sign and encrypt).
    * Select Curve: If choosing ECC, you select the elliptic curve. Curve 25519 is the default.
    * Set Validity: You decide how long the key lasts. 0 means the key does not expire
    * User ID: You must provide a Real Name and Email Address to identify the key.

