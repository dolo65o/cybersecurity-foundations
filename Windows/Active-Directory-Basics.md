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

