## DNS(Domain name system)
DNS (Domain Name System) provides a simple way for us to communicate with devices on the internet without remembering complex numbers.

## Domain Hierarchy

<img width="1140" height="800" alt="dns hierarchy" src="https://github.com/user-attachments/assets/83694f7f-7ade-47c4-83a1-4f2e7239d1e8" />

## TLD (Top-Level Domain)

A TLD is the most righthand part of a domain name. So, for example, the google.com TLD is .com.
* There are two types of TLD ::
  1. gTLD (Generic Top Level) :-  gTLD was meant to tell the user the domain name's purpose; for example, a .com would be for commercial purposes, .org for an organisation.
  2. ccTLD (Country Code Top Level Domain) :- ccTLD was used for geographical purposes, for example, .ca for sites based in Canada, .co.uk for sites based in the United Kingdom and so on.
>  For a full list of over 2000 TLDs [click here](https://data.iana.org/TLD/tlds-alpha-by-domain.txt).

## Second-Level Domain
Taking google.com as an example, the .com part is the TLD, and google is the Second Level Domain. When registering a domain name, the second-level domain is limited to 63 characters + the TLD and can only use a-z 0-9 and hyphens. 

## Subdomain
A subdomain sits on the left-hand side of the Second-Level Domain using a period to separate it; for example, in the name admin.yoursite.com the admin part is the subdomain. You can use multiple subdomains split with periods to create longer names, such as jupiter.servers.yoursite.com. But the length must be kept to 253 characters or less.

## DNS Record Types
Type of instructions written in a domain’s control panel (DNS zone file) that tell the internet what to do with that domain.

Some of the most common ones:
1. A Record (Address Record)
    - Purpose: Connects a domain to an IPv4 address.
    - Example: google.com → 142.250.190.14
2. AAAA Record
    - Purpose: Same as A record, but for IPv6 (newer format IPs).
    - Example: yoursite.com → 2606:4700:20::681a:be5
3. CNAME Record (Canonical Name)
    - Purpose: Points one domain to another domain, not to an IP.
    - Use case:
        - You want blog.yoursite.com to go to yoursite.medium.com.
        - Instead of IP, CNAME points to the domain name.
4. MX Record (Mail Exchange)
    - Purpose: Tells which server handles email for your domain.
    - Example: tryhackme.com → alt1.aspmx.l.google.com
5. TXT Record
    - Purpose: Stores text info – mostly for verification, security, and anti-spam.

> Example:

  * Say you bought dolocyber.com, and you want:
    - A website → Hosted on AWS.
    - Email → Handled by Google Workspace.
    - Blog → On Medium.
  * You’d use:
      - A record: dolocyber.com → [your AWS IP]
      - MX record: dolocyber.com → Google mail servers
      - CNAME: blog.dolocyber.com → dolocyber.medium.com
      - TXT: Add Google verification + SPF settings.
## DNS request

1. **Local Cache**

   * Your computer checks its DNS cache to see if it already knows the IP.
   * If it’s cached, no DNS lookup is needed.

2. **Recursive DNS Server (usually from ISP)**

   * If not cached locally, your request goes to the recursive DNS server.
   * It checks its own cache. If still not found, it starts a full lookup.

3. **Root DNS Server**

   * It’s like the master directory.
   * Says: “You want a `.com` domain? Ask the `.com` TLD server.”

4. **TLD DNS Server**

   * Handles all domains under a TLD (like `.com`, `.net`, `.org`).
   * Replies with the **authoritative name server** for that specific domain.

5. **Authoritative DNS Server**

   * This server **owns the final answer** (A, AAAA, CNAME, MX, etc.).
   * Sends back the correct IP address for the domain.

6. **Back to Client**

   * The recursive DNS sends the IP back to your computer.
   * Your browser connects to that IP, and the website loads.

---

###  Final Flow to Memorize:

```
Local Cache → Recursive DNS → Root DNS → TLD Server → Authoritative DNS → IP → You
```



