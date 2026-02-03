## TLS
Transport Layer Security (TLS) is a cryptographic protocol that provides end-to-end security, privacy, and data integrity for communications over the internet. As the modern, secure successor to SSL, TLS encrypts data between web browsers and servers (HTTPS) or email, preventing tampering and eavesdropping.
- Like SSL, its predecessor, TLS is a cryptographic protocol operating at the OSI model’s transport layer.
- TLS ensures that no one can read or modify the exchanged data.
- Examples include HTTP, DNS, MQTT, and SIP, which have become HTTPS, DoT (DNS over TLS), MQTTS, and SIPS, where the appended “S” stands for Secure due to the use of SSL/TLS.

## TLS Certificates – Key Questions & Answers

### 1. Why does a server need a TLS certificate?
A server needs a TLS certificate to prove its identity to clients. Without a certificate, attackers could impersonate the server and perform man-in-the-middle (MITM) attacks.

---

### 2. What is a Certificate Signing Request (CSR)?
A Certificate Signing Request (CSR) is created by the server administrator and contains the server’s identity information and public key. It is sent to a Certificate Authority so the CA can verify the identity and issue a signed certificate.

---

### 3. What role does a Certificate Authority (CA) play?
A Certificate Authority verifies the identity of the server (such as domain ownership) and digitally signs the certificate. This signature allows others to trust that the certificate is legitimate.

---

### 4. What does it mean when a certificate is “signed”?
A signed certificate means a trusted Certificate Authority has validated the server’s identity and attached its digital signature. This signature is used by clients to verify the authenticity of the certificate.

---

### 5. How does a browser verify a TLS certificate?
The browser checks the certificate’s signature against trusted CA certificates installed on the system. If the signing CA is trusted and the certificate is valid, the secure connection is established; otherwise, a warning is shown.
