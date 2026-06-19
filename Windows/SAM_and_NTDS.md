# SAM and NTDS.dit

## Overview

Windows stores credential information in different locations depending on whether the system is a standalone computer or part of a domain. 

Two important credential stores are:

- SAM (Security Account Manager)
- NTDS.dit (Active Directory Database)

These are common targets during credentials dumping attacks.

---

## What is SAM?

SAM (Security Account Manager) is a Windows database that stores information about local user accounts. 

Examples:

- Administrator
- LocalUser1
- HelpDesk

Location:

```text
C:\Windows\System32\Config\SAM
```

---

## What does SAM store?

SAM stores:

- Local usernames
- Password hashes
- Security information for local accounts

Important:

Windows does not store plaintext passwords in SAM. Instead, it stores password hashes.

Example:

```text
Password123
↓
NTLM Hash
```

---

## Why attackers target SAM?

If attackers gain Administrator privileges, they may attempt to access the SAM database.

Goals:

- Obtain password hashes
- Crack passwords offline
- Reuse credentials

SOC Note:

Unexpected access to the SAM database should be investigated.

---

## What is NTDS.dit?

NTDS.dit is the main Active Directory database.

It exists on Domain Controllers.

Location:

```text
C:\Windows\NTDS\NDS.dit
```

---

## What does NTDS.dit Store?

NTDS.dit stores:

- Domain user accounts
- Password hashes
- Group memberships
- Computer accounts
- Active Directory objects

Examples:

- Domain Users
- Domain Admins
- Service Accounts

---

## Why attackers target NTDS.dit?

NTDS.dit is one of the most valuable files in an Active Directory environment.

If compromised, attackers may obtain:

- Domain account hashes
- Administrator credentials
- Service account credentials

  SOC Note:
  Access to NTDS.dit is considered a major security incident.

  ---

  ## SAM vs NTDS.dit

  | Feature | SAM | NTDS.dit |
  |---------|-----|----------|
  | Stores Local Accounts | Yes | No |
  | Stores Domain Accounts | No | Yes |
  | Found on Workstations | Yes | No |
  | Found on Domain Controllers | Yes | Yes |
  | Contains Password Hashes | Yes | Yes |

  ---

  ## Example Attack Scenario

```text
 Initial Access
   ↓
Privilege Escalation
      ↓
  Access SAM
      ↓
Steal Local Hashes
      ↓
Move Through Network
      ↓
Reach Domain Controller
      ↓
  Access NTDS.dit
      ↓
Steal Domain Hashes
```

---

## Detection Opportunities

Monitor for:

- Credential dumping activity
- Suspicious administrative actions
- Unexpected access to credential stores
- Unusual PowerShell activity
- EDR alerts involving credential access

---

## Investigation Questions

When investigating credential dumping:

- Was SAM accessed?
- Was NTDS.dit accessed?
- Which account performed the action?
- Was privilege escalation observed?
- Were stolen credentials used later?

---
## Quick Summary

| Item | Purpose |
|------|---------|
| SAM | Stores local account information |
| NTDS.dit | Stores Active Directory information |
| Password Hash | Mathematical representation of a password |
| Domain Controller | Server that manages Active Directory |
| Credential Dumping | Extraction of stored credentials |

---

## What is the difference between SAM and NTDS.dit?

SAM stores local account information on Windows systems, while NTDS.dlt stores domain account information within Active Directory. 
     
