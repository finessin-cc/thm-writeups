# TryHackMe: Active Directory Basics

| Field | Details |
|---|---|
| **Platform** | TryHackMe |
| **Room** | Active Directory Basics |
| **Difficulty** | Easy |
| **Estimated Time** | 30 minutes |
| **Category** | Fundamentals / Windows / Active Directory |

---

## Table of Contents

1. [Introduction](#task-1-introduction)
2. [Windows Domains](#task-2-windows-domains)
3. [Active Directory Objects](#task-3-active-directory)
4. [Managing Users in AD](#task-4-managing-users-in-ad)
5. [Managing Computers in AD](#task-5-managing-computers-in-ad)
6. [Group Policies](#task-6-group-policies)
7. [Authentication Methods](#task-7-authentication-methods)
8. [Trees, Forests and Trusts](#task-8-trees-forests-and-trusts)

---

## Task 1: Introduction

Active Directory (AD) is Microsoft's centralised identity and access management service — the de-facto backbone of enterprise Windows environments. This room covers core AD concepts required for both administration and penetration testing of Windows domain environments.

**Room Objectives:**
- Understand what Active Directory is and how it functions
- Understand the structure of an Active Directory Domain
- Identify the core components of an AD Domain
- Understand Forests, Trees, and Domain Trust Relationships

**Prerequisites:** Windows Fundamentals module familiarity.

---

## Task 2: Windows Domains

### Concept Overview

A **Windows Domain** is a logical grouping of users and computers under centralised administration. Rather than managing each machine individually, a domain consolidates identity and policy management into a single service.

| Component | Description |
|---|---|
| **Active Directory (AD)** | Centralised repository holding all network object data |
| **Domain Controller (DC)** | Server running Active Directory Domain Services (AD DS) |
| **Domain** | Administrative boundary grouping users, computers, and policies |

### Key Advantages of a Windows Domain

- **Centralised Identity Management** — User accounts are configured once in AD and are valid across all domain-joined machines.
- **Policy Management** — Security policies are pushed from AD to users and computers network-wide via Group Policy.

### Lab Environment

The lab domain for this room is `THM.local`. Administrative access is provided via RDP:

| Field | Value |
|---|---|
| **Username** | `THM\Administrator` |
| **Password** | `Password321` |
| **IP** | `MACHINE_IP` |

### Task Answers

| Question | Answer |
|---|---|
| Credentials are stored in a centralised repository called... | `Active Directory` |
| The server in charge of running Active Directory services is called... | `Domain Controller` |

---

## Task 3: Active Directory

### AD DS — Active Directory Domain Services

The **Active Directory Domain Service (AD DS)** acts as a catalogue of all objects on the network. An "object" is any resource that AD manages — users, computers, printers, shares, groups, etc.

### Core Object Types

#### Users (Security Principals)

Users are **security principals** — they can be authenticated and assigned privileges over resources.

| User Type | Description |
|---|---|
| **People** | Represent employees or persons needing network access |
| **Service Accounts** | Run services like IIS or MSSQL with minimum required privileges |

#### Machine Accounts (Security Principals)

Every computer that joins an AD domain receives a **machine object**. Machine accounts are local administrators of their respective computers.

- Machine account naming convention: `MACHINENAME$`
- Example: A computer named `DC01` has account `DC01$`
- Passwords are **120 random characters**, rotated automatically

#### Security Groups (Security Principals)

Groups are used to assign access rights to resources en masse. Groups can contain users, machines, and other groups.

**Default Domain Security Groups:**

| Group | Description |
|---|---|
| `Domain Admins` | Full administrative control over the entire domain, including all DCs |
| `Server Operators` | Can administer DCs but cannot change administrative group memberships |
| `Backup Operators` | Can access any file regardless of permissions; used for backup operations |
| `Account Operators` | Can create and modify domain user accounts |
| `Domain Users` | Contains all user accounts in the domain |
| `Domain Computers` | Contains all computer accounts in the domain |
| `Domain Controllers` | Contains all Domain Controllers in the domain |

### Organisational Units (OUs)

OUs are **container objects** used to organise users and machines. They reflect the company's structure and are used for targeted Group Policy application.

- A user can belong to **only one OU** at a time
- Default containers created by Windows:

| Container | Contents |
|---|---|
| `Builtin` | Default groups available on any Windows host |
| `Computers` | Default placement for all newly joined machines |
| `Domain Controllers` | Default OU for all DCs |
| `Users` | Default domain-wide users and groups |
| `Managed Service Accounts` | Accounts used by domain services |

### Security Groups vs. OUs

| Feature | OUs | Security Groups |
|---|---|---|
| **Purpose** | Apply policies (GPOs) to users/computers | Grant permissions over resources |
| **Membership** | User in **one OU only** | User can be in **multiple groups** |
| **Use Case** | Department-specific configurations | Shared folder or printer access |

### Task Answers

| Question | Answer |
|---|---|
| Which group normally administrates all computers and resources in a domain? | `Domain Admins` |
| Machine account name for `TOM-PC`? | `TOM-PC$` |
| Container type for grouping QA users for policy application? | `Organizational Units` |

---

## Task 4: Managing Users in AD

### Deleting OUs — Accidental Deletion Protection

By default, OUs are protected from accidental deletion. To remove an OU:

1. Open **Active Directory Users and Computers**
2. Enable **View → Advanced Features**
3. Right-click the OU → **Properties** → **Object tab**
4. Uncheck **"Protect object from accidental deletion"**
5. Right-click the OU → **Delete**

> **Note:** Deleting an OU also deletes all users, groups, and sub-OUs contained within it.

### Delegation

**Delegation** allows granting specific administrative privileges over OUs to non-admin users — without making them Domain Admins.

**Common use case:** Granting IT support the ability to reset passwords for users in specific OUs.

**To delegate control over an OU:**
1. Right-click the target OU → **Delegate Control**
2. Add the user (e.g., `phillip`) via **Check Names**
3. Select the delegated task (e.g., **Reset user passwords and force password change at next logon**)

### Resetting a Password via PowerShell (Delegated User)

Logged in as `THM\phillip` (delegated IT support):

```powershell
# Reset Sophie's password
PS C:\Users\phillip> Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose

New Password: *********

VERBOSE: Performing the operation "Set-ADAccountPassword" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```

```powershell
# Force password change at next logon
PS C:\Users\phillip> Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose

VERBOSE: Performing the operation "Set" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```

**Phillip's Credentials (for lab):**

| Field | Value |
|---|---|
| Username | `THM\phillip` |
| Password | `Claire2008` |

### Task Answers

| Question | Answer |
|---|---|
| Flag found on Sophie's desktop? | `THM{REDACTED}` |
| The process of granting privileges to a user over an OU is called...? | `delegation` |

---

## Task 5: Managing Computers in AD

### Default Behaviour

All domain-joined machines (except DCs) are placed in the default **`Computers`** container. This is not optimal as it prevents granular policy application across different device types.

### Recommended Device Segregation

| Category | Description |
|---|---|
| **Workstations** | End-user devices for daily tasks; privileged accounts should never be signed in |
| **Servers** | Provide services to users or other servers |
| **Domain Controllers** | Most sensitive devices; contain hashed passwords for all domain accounts |

### Lab Task

Two new OUs were created directly under `thm.local`:

```
thm.local
├── Workstations     ← Personal computers and laptops (7 devices)
├── Servers          ← Server machines
└── Domain Controllers (pre-existing, Windows-managed)
```

Machines were moved from the default `Computers` container into the appropriate OU.

### Task Answers

| Question | Answer |
|---|---|
| How many computers ended up in the Workstations OU? | `7` |
| Is it recommendable to create separate OUs for Servers and Workstations? | `yay` |

---

## Task 6: Group Policies

### Group Policy Objects (GPOs)

**GPOs** are collections of configuration settings applied to OUs. They can target **users**, **computers**, or both.

**GPO Management Tool:** Start Menu → **Group Policy Management**

### GPO Distribution

GPOs are distributed via the **`SYSVOL`** network share, hosted on the Domain Controller.

| Detail | Value |
|---|---|
| Share Name | `SYSVOL` |
| Default Path on DC | `C:\Windows\SYSVOL\sysvol\` |
| Sync Interval | Up to 2 hours |

```powershell
# Force immediate GPO sync on a machine
PS C:\> gpupdate /force
```

### Pre-existing GPOs in the Lab

| GPO Name | Linked To |
|---|---|
| `Default Domain Policy` | `thm.local` (entire domain) |
| `RDP Policy` | `thm.local` (entire domain) |
| `Default Domain Controllers Policy` | `Domain Controllers` OU only |

> GPOs apply to the linked OU **and all child OUs** beneath it.

### Modifying Minimum Password Length

**Path:** `Computer Configurations → Policies → Windows Settings → Security Settings → Account Policies → Password Policy`

Set **Minimum Password Length** to `10 characters`.

### Lab GPO Implementation

#### GPO 1: Restrict Control Panel Access

**Objective:** Block non-IT users from accessing the Control Panel.

**Policy Path:** `User Configuration → Administrative Templates → Control Panel → Prohibit Access to Control Panel and PC settings` → **Enabled**

**Linked to OUs:** `Sales`, `Marketing`, `Management`

**Not applied to:** `IT` OU (IT users retain Control Panel access)

#### GPO 2: Auto Lock Screen

**Objective:** Lock workstations and servers after 5 minutes of inactivity.

**Policy Path:** `Computer Configuration → Policies → Windows Settings → Security Settings → Local Policies → Security Options → Interactive Logon: Machine inactivity limit` → **300 seconds (5 minutes)**

**Linked to:** Root domain `thm.local` (inherited by all child OUs — Workstations, Servers, Domain Controllers)

> **Note:** Computer Configuration settings are ignored for OUs containing only user objects (e.g., Sales, Marketing).

### Verification — Mark's Account (Marketing)

| Field | Value |
|---|---|
| Username | `THM\Mark` |
| Password | `M4rk3t1ng.21` |

Logging in as `THM\Mark` and attempting to open Control Panel produces:

```
This operation has been cancelled due to restrictions in effect on this computer.
Please contact your system administrator.
```

### Task Answers

| Question | Answer |
|---|---|
| Network share used to distribute GPOs? | `sysvol` |
| Can a GPO apply settings to both users and computers? | `yay` |

---

## Task 7: Authentication Methods

Windows domains support two network authentication protocols:

| Protocol | Status | Description |
|---|---|---|
| **Kerberos** | Current default | Ticket-based authentication used by all modern Windows versions |
| **NetNTLM** | Legacy / Compatibility | Challenge-response mechanism; kept for backward compatibility |

---

### Kerberos Authentication

Kerberos is the **default protocol** in any modern Windows domain. It uses a **ticket-based** system to avoid transmitting credentials repeatedly.

#### Step 1 — TGT Request

```
Client  ──[Username + Encrypted Timestamp]──►  KDC (Domain Controller)
        ◄──[TGT + Session Key]────────────────
```

- The client encrypts a timestamp using a key derived from their password
- The **Key Distribution Center (KDC)** (running on the DC) issues a **Ticket Granting Ticket (TGT)**
- The TGT is encrypted with the **`krbtgt` account's password hash** — the client cannot read it
- A **Session Key** is returned alongside the TGT for future requests

#### Step 2 — TGS Request

```
Client  ──[TGT + SPN + Encrypted Username/Timestamp]──►  KDC
        ◄──[TGS + Service Session Key]──────────────────
```

- The client presents the TGT and a **Service Principal Name (SPN)** to identify the target service
- The KDC returns a **Ticket Granting Service (TGS)** encrypted with the **Service Owner's password hash**
- A **Service Session Key** is included for authenticating to the target service

#### Step 3 — Service Authentication

```
Client  ──[TGS]──►  Target Service
                    (Decrypts TGS using its own password hash, validates Service Session Key)
```

---

### NetNTLM Authentication

NetNTLM uses a **challenge-response** mechanism. The user's password hash is **never transmitted** over the network.

```
Client  ──[1. Auth Request]──────────────────────────►  Server
        ◄──[2. Random Challenge]──────────────────────
Client  ──[3. Response = NTLM_Hash ⊕ Challenge]──────►  Server
                                                         ──[4. Challenge + Response]──►  DC
                                                         ◄──[5. Auth Result]──────────
        ◄──[6. Auth Result]──────────────────────────
```

| Step | Action |
|---|---|
| 1 | Client sends authentication request to server |
| 2 | Server sends a random **challenge** number |
| 3 | Client computes **response** using NTLM hash + challenge |
| 4 | Server forwards challenge + response to **Domain Controller** |
| 5 | DC recalculates expected response and compares; returns result |
| 6 | Server relays authentication result to client |

> **Note:** For **local accounts**, the server validates the response itself using its local **SAM database** — no DC interaction required.

### Task Answers

| Question | Answer |
|---|---|
| Will a current Windows version use NetNTLM as the preferred protocol by default? | `nay` |
| What ticket type allows requesting further TGS tickets in Kerberos? | `Ticket Granting Ticket` |
| Is a user's password transmitted over the network with NetNTLM? | `nay` |

---

## Task 8: Trees, Forests and Trusts

As organisations grow, a single domain often becomes insufficient. AD supports multi-domain architectures through Trees, Forests, and Trust Relationships.

---

### Trees

A **Tree** is a collection of domains that **share the same namespace**, joined in a parent-child hierarchy.

```
thm.local              ← Root Domain
├── uk.thm.local       ← Child Domain (UK branch)
└── us.thm.local       ← Child Domain (US branch)
```

- Each domain in the tree has its **own DC** and manages its own resources independently
- A new group is introduced: **`Enterprise Admins`** — administrative privileges across **all** domains in the enterprise

| Group | Scope |
|---|---|
| `Domain Admins` | Administrative control over a **single** domain |
| `Enterprise Admins` | Administrative control over **all** domains in the enterprise |

---

### Forests

A **Forest** is the union of multiple Trees with **different namespaces** into a single AD environment — typically seen after company mergers or acquisitions.

```
Forest
├── thm.local Tree
│   ├── uk.thm.local
│   └── us.thm.local
└── mht.local Tree
    ├── eu.mht.local
    └── asia.mht.local
```

---

### Trust Relationships

**Trust Relationships** allow users from one domain to access resources in another domain.

#### One-Way Trust

```
Domain AAA  ──[Trusts]──►  Domain BBB
```

- Users in **BBB** can be authorised to access resources in **AAA**
- The direction of trust is **opposite** to the direction of access

#### Two-Way Trust

```
Domain AAA  ◄──[Mutual Trust]──►  Domain BBB
```

- Both domains mutually authorise each other's users
- **Default** when joining domains under a Tree or Forest

> **Important:** A trust relationship does **not** automatically grant access to all resources. It provides the *capability* to authorise cross-domain access — what is actually permitted must be explicitly configured.

### Task Answers

| Question | Answer |
|---|---|
| A group of Windows domains sharing the same namespace is called a...? | `Tree` |
| What must be configured for a user in Domain A to access a resource in Domain B? | `A Trust Relationship` |

---

## Summary of Key Concepts

| Concept | Key Takeaway |
|---|---|
| **Active Directory** | Centralised identity and resource management for Windows domains |
| **Domain Controller** | Server hosting AD DS; central authority for authentication and policy |
| **OUs** | Organisational containers for applying GPOs; users belong to one OU only |
| **Security Groups** | Resource access control; users can belong to many groups |
| **Delegation** | Grants scoped AD admin rights without Domain Admin privileges |
| **GPO** | Policy objects linked to OUs; distributed via `SYSVOL` share |
| **Kerberos** | Default ticket-based auth protocol; uses TGT → TGS flow |
| **NetNTLM** | Legacy challenge-response auth; no password transmitted |
| **Tree** | Domains sharing the same namespace in a hierarchy |
| **Forest** | Multiple trees with different namespaces in one AD environment |
| **Trust** | Enables cross-domain resource authorisation; can be one-way or two-way |
