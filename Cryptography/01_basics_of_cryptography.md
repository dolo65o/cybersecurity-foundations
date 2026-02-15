# Cryptography Essentials 

Cryptography is the practice and study of techniques for secure communication in the presence of adversaries. Its ultimate goal is to ensure that data remains confidential and intact, preventing unauthorized parties from disclosing or altering the message.

---

## 1. Core Objectives 

Cryptography is used to protect three main pillars of security:
* **Confidentiality**: Keeping data secret from unauthorized snooping.
* **Integrity**: Ensuring data has not been altered or tampered with.
* **Authenticity**: Verifying the identity of the communicating parties.

---

## 2. Real-World Use Cases 

You rarely interact directly with cryptography, but it powers security behind the scenes in daily activities:

* **User Login**: Credentials are encrypted before being sent to the server, preventing attackers from intercepting passwords.
* **Remote Access (SSH)**: SSH clients establish an **encrypted tunnel**, ensuring no one can eavesdrop on the command session.
* **Online Banking**: Browsers use certificates to verify the identity of the bank's server, ensuring you aren't talking to an attacker.
* **File Downloads**: Hash functions are used to verify that a downloaded file is identical to the original and hasn't been corrupted or modified.

---

## 3. Compliance & Standards 

Different industries have legal frameworks requiring the use of cryptography to protect sensitive data.

### Payment Card Industry (Financial) 
* **Standard**: **PCI DSS** (Payment Card Industry Data Security Standard).
* **Requirement**: Ensures a minimum level of security for storing, processing, and transmitting credit card data.
* **Encryption Rule**: Data must be encrypted both **at rest** (storage) and **in motion** (transmission).

### Medical & Data Privacy (Healthcare/General) 
Regulations for handling medical records and personal data vary by country:

| Region | Regulation | Full Name |
| :--- | :--- | :--- |
| **USA** 🇺🇸 | **HIPAA** | Health Insurance Portability and Accountability Act |
| **USA** 🇺🇸 | **HITECH** | Health Information Technology for Economic and Clinical Health |
| **EU** 🇪🇺 | **GDPR** | General Data Protection Regulation |
| **UK** 🇬🇧 | **DPA** | Data Protection Act |

> **Summary**: These laws demonstrate that cryptography is not just a technical tool but a legal necessity for protecting user privacy and sensitive records.

---

## Core Process
1. Begin with the plaintext that we want to encrypt.( it can be anything from a simple “hello”, a cat photo, credit card information, or medical health records)
2. The plaintext is passed through the encryption function along with a proper key.
3. The encryption function returns a ciphertext.
4. The encryption function is part of the cipher; a cipher is an algorithm to convert a plaintext into a ciphertext and vice versa.
   
   <img width="914" height="458" alt="cryptography encryption" src="https://github.com/user-attachments/assets/ae9f52aa-1173-4f18-b24f-37565205ab10" />

5. To recover the plaintext, we must pass the ciphertext along with the proper key via the decryption function, which would give us the original plaintext.

     <img width="909" height="451" alt="cryptography Decryption" src="https://github.com/user-attachments/assets/06fd0e87-45a2-4e6a-842f-fef61bc15271" />

   
### Key Terminology

* **Plaintext:** This refers to the original, readable message or data before it is encrypted. It can be anything from a text document to an image or multimedia file.
* **Ciphertext:** The scrambled, unreadable result of encryption. Ideally, it should reveal no information about the original message other than its approximate size.
* **Cipher:** The algorithm or method used to convert plaintext into ciphertext and vice versa. These algorithms are typically developed by mathematicians.
* **Key:** A string of bits that the cipher uses to encrypt or decrypt data. While the cipher method is usually public knowledge, the key must remain secret to ensure security.
* **Encryption:** The process of converting plaintext into ciphertext using a cipher and a key. The choice of cipher is generally disclosed, unlike the key.
* **Decryption:** The reverse process that converts ciphertext back into plaintext. Recovering the plaintext without the key should be computationally infeasible.

---

# Historical Ciphers: The Caesar Cipher 

While cryptography dates back to Ancient Egypt (1900 BCE), one of the most famous historical examples is the **Caesar Cipher** from the first century BCE.

---

## Mechanism: How it Works 
The Caesar Cipher is a simple substitution technique.

* **Logic:** It shifts each letter of the alphabet by a fixed number (the Key) to encrypt the message.
* **Encryption (Right Shift):** To encrypt, you shift the letters to the **right**.
    * *Example:* `A` with Key `3` becomes `D`.
* **Decryption (Left Shift):** To decrypt, you shift the letters back to the **left** by the same number.
* **Looping:** If the shift goes past `Z`, it wraps around to the start (`A`).

### Example 
* **Plaintext:** `TRYHACKME`
* **Key:** `3` (Right shift)
* **Result:** `T` becomes `W`, `R` becomes `U`, etc.
* **Ciphertext:** `WUBKDFNPH`

---

## Security Weaknesses 
By modern standards, the Caesar Cipher is considered completely insecure.

* **Limited Keys:** The English alphabet has 26 letters. Shifting by 26 results in the original text, leaving only **25 possible keys**.
* **Brute Force Vulnerability:** Because the "Key Space" (number of possible keys) is so small, an attacker can easily try every single option until the message makes sense.

---


## Other Notable Historical Ciphers
You may encounter these other classical methods in cryptography history:

* **The Vigenère Cipher:** A more complex polyalphabetic cipher from the 16th century.
* **The Enigma Machine:** The electromechanical encryption device used by Germany in World War II.
* **The One-Time Pad:** A theoretically unbreakable cipher used during the Cold War.

---

# Modern Encryption Types

Modern cryptography is divided into two primary categories based on how keys are managed: Symmetric and Asymmetric encryption.

## 1. Symmetric Encryption
Also known as **Private Key Cryptography**.

* **Mechanism:** It uses the **same key** to both encrypt and decrypt the data.
* **Key Security:** Keeping the key secret is mandatory. If an attacker gains access to the key, they can decrypt all data.
* **The Distribution Challenge:** The biggest difficulty is securely sharing the key with the recipient without it being intercepted. For example, you can email an encrypted file, but you cannot safely email the password to open it.

### Common Symmetric Algorithms
* **DES (Data Encryption Standard):** Adopted in 1977. It uses a **56-bit key**, which is now considered insecure; it was successfully broken in less than 24 hours in 1999.
* **3DES (Triple DES):** Applied DES three times to increase security. It uses a **168-bit key** (effective security of 112 bits). It was deprecated in 2019 and is generally found only in legacy systems.
* **AES (Advanced Encryption Standard):** Adopted in 2001 as the replacement for DES/3DES. It supports key sizes of **128, 192, or 256 bits** and is the current standard.

---

## 2. Asymmetric Encryption
Also known as **Public Key Cryptography**.

* **Mechanism:** Unlike symmetric encryption, this uses a **pair of keys**.
    * **Public Key:** Shared with everyone. Used to **encrypt** data.
    * **Private Key:** Kept secret. Used to **decrypt** data.
* **Mathematical Basis:** It relies on mathematical problems that are easy to calculate in one direction but practically infeasible to reverse (e.g., taking millions of years to solve).
* **Performance:** It is generally **slower** than symmetric encryption and requires larger key sizes.

### Common Asymmetric Algorithms
* **RSA:** One of the most common standards. It uses large key sizes, with **2048 bits** being the recommended minimum (3072 and 4096 bits are also used).
* **Diffie-Hellman:** Widely used for key exchange. Like RSA, it recommends a minimum key size of 2048 bits.
* **ECC (Elliptic Curve Cryptography):** A modern approach that achieves high security with much smaller keys. For example, a **256-bit ECC key** provides comparable security to a **3072-bit RSA key**.

---

# Cryptography Math: XOR & Modulo 

Modern cryptography relies heavily on mathematics. Two specific operations are fundamental to many algorithms: the **XOR** operation and the **Modulo** operation.

---

## 1. The XOR Operation ($\oplus$) 
**XOR** (Exclusive OR) is a logical operation in binary arithmetic.

* **Logic:** It compares two bits:
    * Returns `1` if the bits are **different**.
    * Returns `0` if the bits are the **same**.
* **Symbol:** Often represented by $\oplus$ or `^`.

### Truth Table
| Input A | Input B | Output ($A \oplus B$) |
| :---: | :---: | :---: |
| 0 | 0 | **0** |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | **0** |


### Why it Matters for Encryption
XOR has unique properties that make it perfect for reversible encryption:
1.  **Identity:** $A \oplus 0 = A$ (XORing with 0 preserves the value).
2.  **Self-Inverse:** $A \oplus A = 0$ (XORing a value with itself "cancels" it out).

**Encryption Logic:**
If you have a Plaintext ($P$) and a Secret Key ($K$), you can create Ciphertext ($C$):
$$C = P \oplus K$$

**Decryption Logic:**
To get the message back, you simply XOR the Ciphertext with the Key again:
$$C \oplus K = (P \oplus K) \oplus K = P \oplus 0 = P$$

---

## 2. The Modulo Operation (%) 
The modulo operator, written as `%` or `mod`, calculates the **remainder** of a division operation.

* **Logic:** For equation $X \% Y$, it returns the remainder when $X$ is divided by $Y$.
* **Examples:**
    * $25 \% 5 = 0$ (because $25 = 5 \times 5 + 0$).
    * $23 \% 6 = 5$ (because $23 = 6 \times 3 + 5$).
    * $23 \% 7 = 2$ (because $23 = 7 \times 3 + 2$).

### Why it Matters for Cryptography
1.  **Irreversibility (One-Way Function):** Modulo is not fully reversible. If you know $x \% 5 = 4$, you cannot determine exactly what $x$ was (it could be 4, 9, 14, etc.). This property is crucial for algorithms like RSA and Diffie-Hellman.
2.  **Fixed Range:** The result of $a \% n$ will **always** be a number between $0$ and $n-1$. This ensures cryptographic outputs stay within a predictable size.
