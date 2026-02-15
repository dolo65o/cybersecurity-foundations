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

   <img width="909" height="484" alt="cryptography Decryption" src="https://github.com/user-attachments/assets/cb9a2532-829a-45a3-a0ae-d00bac7c4477" />
   
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

## 1. Mechanism: How it Works 
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

## 2. Security Weaknesses 
By modern standards, the Caesar Cipher is considered completely insecure.

* **Limited Keys:** The English alphabet has 26 letters. Shifting by 26 results in the original text, leaving only **25 possible keys**.
* **Brute Force Vulnerability:** Because the "Key Space" (number of possible keys) is so small, an attacker can easily try every single option until the message makes sense.


---

## 3. Other Notable Historical Ciphers
You may encounter these other classical methods in cryptography history:

* **The Vigenère Cipher:** A more complex polyalphabetic cipher from the 16th century.
* **The Enigma Machine:** The electromechanical encryption device used by Germany in World War II.
* **The One-Time Pad:** A theoretically unbreakable cipher used during the Cold War.
