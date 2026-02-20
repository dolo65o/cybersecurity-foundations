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

