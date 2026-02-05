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

---

## HTTP Over TLS
HTTPS stands for Hypertext Transfer Protocol Secure. It is basically HTTP over TLS. Consequently, requesting a page over HTTPS will require the following three steps (after resolving the domain name):

1. Establish a TCP three-way handshake with the target server
2. Establish a TLS session
3. Communicate using the HTTP protocol; for example, issue HTTP requests, such as GET / HTTP/1.1

---
## SMTP, POP3, and IMAP 
Adding TLS to SMTP, POP3, and IMAP is no different than adding TLS to HTTP. Similar to how HTTP gets an appended S for Secure and becomes HTTPS, SMTP, POP3, and IMAP become SMTPS, POP3S, and IMAPS, respectively. Using these protocols over TLS is no different than using HTTP over TLS
1. The insecure versions use the default TCP port numbers

   
| Protocol | Default Port Number |
|----------|---------------------|
| HTTP     | 80                  |
| SMTP     | 25                  |
| POP3     | 110                 |
| IMAP     | 143                 |

2. The secure versions, i.e., over TLS,
   
| Protocol | Secure Port Number(s) |
|----------|-----------------------|
| HTTPS    | 443                  |
| SMTPS   | 465, 587              |
| POP3S   | 995                   |
| IMAPS   | 993                   |

---

## Secure Shell (SSH)

Secure Shell (SSH) is a cryptographic network protocol developed by Tatu Ylönen in 1995 to provide secure communication over an unsecured network. SSH was created to address the vulnerabilities of earlier remote login protocols, such as Telnet, which transmitted data, including passwords, in plain text, making it susceptible to eavesdropping. SSH encrypts the data transmitted between a client and server, ensuring confidentiality and integrity.
- It is most likely based on OpenSSH libraries and source code.
    - **Secure authentication**: Besides password-based authentication, SSH supports public key and two-factor authentication.
    - **Confidentiality**: OpenSSH provides end-to-end encryption, protecting against eavesdropping.
    - **Integrity**: In addition to protecting the confidentiality of the exchanged data, cryptography also protects the integrity of the traffic.
    - **Tunneling**: SSH can create a secure “tunnel” to route other protocols through SSH. This setup leads to a VPN-like connection.
    - **X11 Forwarding**: If you connect to a Unix-like system with a graphical user interface, SSH allows you to use the graphical application over the network.

---
## SFTP and FTPS
SFTP (SSH File Transfer Protocol) and FTPS (FTP Secure) are both secure methods for transferring files, but they use different underlying technologies: SFTP runs over SSH (Secure Shell), encrypting everything in one channel, making it simpler for firewalls (usually Port 22). FTPS is FTP with SSL/TLS encryption, adding security to the older FTP structure, but it often requires multiple ports (like 990 and dynamic data ports), complicating firewall rules. 

---

## VPN
A virtual private network, or VPN, is an encrypted connection over the Internet from a device to a network.The encrypted connection helps ensure that sensitive data is safely transmitted. It prevents unauthorised people from eavesdropping on the traffic and allows the user to conduct work remotely.VPN technology is widely used in corporate environments.

> Example:- Consider a company with offices in different geographical locations. Can this company connect all its offices and sites to the main branch so that any device can access the shared resources as if physically located in the main branch?
> The answer is yes; furthermore, the most economical solution would be setting up a virtual private network (VPN) using the Internet infrastructure. 
  
