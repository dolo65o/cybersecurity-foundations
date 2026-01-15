# Active Directory (AD)
Active Directory is a directory service developed by Microsoft for Windows domain networks. It stores information about network objects such as computers, users, and groups. It provides authentication and authorisation services, and allows administrators to manage network resources centrally.

## Domain Controller (DC)

A domain controller is a server that manages security authentication requests in a Windows Server network. It stores user account information and controls access to resources on the network. It is a critical component for managing and securing a network infrastructure.

<p align="center">
<img width="452" height="362" alt="Active directory" src="https://github.com/user-attachments/assets/da1ac36a-ac5b-484b-bff7-22cce7a0ba07" />
</p>

> A Real-World Example :- In school/university networks, you will often be provided with a username and password that you can use on any of the computers available on campus. Your credentials are valid for all machines because whenever you input them on a machine, it will forward the authentication process back to the Active Directory, where your credentials will be checked.

## Active Directory Domain Service (ADDS)

- AD DS is the core service of Active Directory.
- It stores and manages all objects in a Windows domain.
- Objects include users, computers, groups, and policies.
- Active Directory Objects:-
  
**1. Users**
  - Users are security principals (can log in and get permissions).
  - Two types of users:
    - Human users → real people (employees, students)
    - Service accounts → used by applications/services
  - Service accounts run services with limited privileges (least privilege).
    
**2. Machines (Computer Accounts)**
  - Every computer that joins a domain gets a machine account.
  - Machines are also security principals.
  - Machine account name ends with `$`
    - Example: `PC01$`, `DC01$`
  - Machine passwords are: auto-generated,very long,automatically changed.
  - Machines authenticate to the domain just like users.
    
**3. Security Groups**
  - Groups are used to assign permissions.
  - Permissions are given to groups, not individual users.
  - Groups can contain:
    - users
    - machines
    - other groups
  - A user can be part of multiple groups.

## Organizational Units (OUs)

* OUs are containers used to organize users and computers.
* OUs are mainly used to apply policies (Group Policy).
* A user or computer can belong to only one OU.
* OUs often reflect company structure (IT, HR, Sales).

> OU controls policies, Groups control access, Users and Machines authenticate, and AD DS manages everything centrally.

## Security Groups vs OUs

Both are used to classify users and computers, their purposes are entirely different:
- OUs are handy for applying policies to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise.
- Security Groups, on the other hand, are used to grant permissions over resources.

## AD OU Management & Delegation

- Organizational Units (OUs) are containers in Active Directory used to organize users and computers and apply policies (GPOs).
- By default, OUs are protected from accidental deletion. To delete an OU, enable View → Advanced Features, then uncheck “Protect object from accidental deletion” in OU properties.
- Delegation allows assigning limited administrative tasks (like password resets) to non-domain admins on specific OUs, following least privilege.
  - Example: IT Support user can be delegated permission to reset passwords for users in Sales/Marketing without full Domain Admin rights.
- Delegated tasks can be executed via PowerShell (e.g., `Set-ADAccountPassword`, `Set-ADUser -ChangePasswordAtLogon`).

## Group Policy Objects (GPO)

Group Policy Object (GPO) is a feature in Windows Server that allows administrators to control user and computer settings across the network. It provides a centralised way to manage and configure operating systems, applications, and user settings.

## Windows Domain Authentication

- Domain Controllers store and verify domain credentials.
- Servers ask the DC to authenticate users.

Two protocols can be used for network authentication in windows domains:

### **Kerberos**

Kerberos works like entry passes and wristbands, not passwords again and again.
  - Uses tickets instead of passwords.
  - Main components:
    - KDC (on Domain Controller):- a crucial component in the Kerberos authentication protocol. It is responsible for issuing Kerberos tickets.
    - TGT (Ticket Granting Ticket):- as a user's proof of authentication and allows a user to request service tickets from the KDC.
    - TGS (Service Ticket):- a component of the Kerberos authentication protocol that enables users to obtain service-specific tickets after they have been authenticated.

---
**STEP 1 & 2: Getting the Ticket Granting Ticket (TGT)**

> **This happens right after user logs in**

<img width="1047" height="416" alt="kerberos 1" src="https://github.com/user-attachments/assets/a495900d-354c-4a88-a874-4ecb8e234f0c" />

#### What Happens
1. User logs in
2. Computer creates a **hash from the password**
3. Computer asks Domain Controller:
   > “Hey, I’m user X. Can I get permission to request services?”

4. Domain Controller checks:
   - Does this user exist?
   - Is the password correct?

5. If yes, DC sends back:
   - **TGT** (locked with krbtgt key → user can’t open it)
   - **Session Key** (user CAN open this)

#### Why This Matters

- User proves identity **once**
- Password is **never sent**
- TGT is valid for several hours

---

**STEP 3 & 4: Requesting a Service Ticket (TGS)**

> **Used when accessing a service like SQL, File Server, Web App**

<img width="1049" height="486" alt="kerberos 2" src="https://github.com/user-attachments/assets/3dcdd591-fecf-4a93-87d2-32403b9e08d0" />

#### What Happens
1. User wants to access a service (example: SQL Server)
2. Client sends to DC:
   - TGT
   - Service name (SPN = MSSQL/SRV)
3. DC checks:
   - Is the TGT valid?
   - Is user allowed to access this service?

4. DC sends back:
   - **Service Ticket (TGS)** → locked with service’s password
   - **Service Session Key**

#### Key Insight (Important)

- User **still never talks to the service directly**
- DC acts like a **trusted gatekeeper**

---

**STEP 5: Authenticating to the Service**

> **Final step — user talks to the service**

<img width="1029" height="362" alt="kerberos 3" src="https://github.com/user-attachments/assets/6e0ccdf8-1f05-43c2-a1b7-6a65e265334f" />

#### What Happens

1. Client sends to service:
   - Service Ticket
   - Timestamp encrypted with Service Session Key

2. Service:
   - Opens ticket using **its own password**
   - Confirms user identity

3. Access is granted

#### Simple Analogy

- **TGT** = ID card
- **TGS** = Entry pass for a specific room
- **Service** checks pass → lets you in

---

## NetNTLM Authentication  
NetNTLM works using a challenge-response mechanism. Windows New Technology LAN Manager (NTLM) is a suite of security protocols offered by Microsoft to authenticate users’ identity and protect the integrity and confidentiality of their activity.

<img width="1051" height="605" alt="NetNTLM Authentication" src="https://github.com/user-attachments/assets/3c8f0cbc-3e5b-4a67-9a4a-02757e566b68" />

### Step-by-Step 

1. **Client → Server**  
   Requests access to a service.

2. **Server → Client**  
   Sends a random **challenge**.

3. **Client → Server**  
   Encrypts the challenge using the **NTLM hash** and sends the **response**.

4. **Server → Domain Controller**  
   Forwards username, challenge, and response.

5. **Domain Controller**  
   Recreates the response using stored NTLM hash.

6. **Allow / Deny**  
   If responses match → access allowed.

---

## Active Directory Structure

### Single Domain

<img width="641" height="384" alt="Single Domain" src="https://github.com/user-attachments/assets/93770097-21a7-42ae-ade7-48a016565dfc" />

A domain is the most basic unit in Active Directory.

Key points:
- Managed by a Domain Controller (DC)
- Stores users, computers, and servers
- Central place for authentication and policies
- Example domain name: `thm.local`

> Single domains work well for small organizations, but become hard to manage as the company grows and expands to new locations.
 
---

## Domain Tree

<img width="1218" height="963" alt="Domain Tree" src="https://github.com/user-attachments/assets/2fec191f-04b2-4b4a-88c5-06811e987b49" />


A domain tree is a collection of related domains that share the same name structure.

Key points:
- One root domain controls the tree
- Child domains extend the root domain
- All domains share the same namespace

Example:
- Root domain: `thm.local`
- Child domains:
  - `uk.thm.local`
  - `us.thm.local`

Each child domain can manage its own users and policies without affecting other domains.

---

## Forest

<img width="2778" height="1119" alt="Forest" src="https://github.com/user-attachments/assets/81461c46-7598-4e7c-becb-2e70d1bd46f5" />

A forest is the highest level structure in Active Directory.

Key points:
- Contains multiple domain trees
- Trees have different namespaces
- Common when companies merge or grow large

Example:
- One tree uses `thm.local`
- Another tree uses `mht.local`

Enterprise Admins have administrative control across the entire forest.

---

## Trust Relationships

<img width="963" height="386" alt="Trust Relationships" src="https://github.com/user-attachments/assets/572bc80f-d5cb-4c50-91bf-97a0a76682c7" />

Trust relationships allow users from one domain to access resources in another domain.

Key points:
- Trust does not automatically grant access.
- Permissions must be configured manually.
- Used to share resources across domains or forests.

One-way trust:
- Domain A trusts Domain B.
- Users from Domain B can access Domain A resources.
- Access direction is opposite to trust direction.

Two-way trust:
- Both domains trust each other.
- Users from both domains can access shared resources.
- Default behavior inside trees and forests.

---

