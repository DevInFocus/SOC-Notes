# Active Directory Basics

## Overview

Active Directory (AD) is a directory service used by Windows environments to centrally manage users, computers, groups, and security policies. Instead of managing each computer individually, administrators can manage everything from a central location

SOC Note:
Active Directory is one of the most important components in enterprise environments and is frequently targeted by attackers

---

## Why Active Directory Exists?

Without Active Directory:

```text
PC1 -> Separate User Accounts
PC2 -> Separate User Accounts
PC3 -> Separate User Accounts
```

Administrators must manage each computer individually.

With Active Directory:

```text
     
        
         Domain Controller
                    │
      ┌─────────────┼─────────────┐
      │             │             │
     PC1           PC2           PC3
```

Users and computers are managed from one central location.

---

## Domain

A Domain is a group of computers and users managed togther.

Example:

```text
company.local
```

All users and systems belong to the same domain.

Examples:

- User Accounts
- Workstations
- Servers
- Domain Controllers

---

## Domain Controller (DC)

A Domain Controller is a server that manages Active Directory.

Responsibilties:

- User authentication
- User management
- Group management
- Password policies
- Access control

SOC Note:
Domain Controllers are among the most crticial systems in an organization.

---

## Active Directory Objects

Everything inside Active Directory is stored as an object.

Examples:

### User Objects

```text
John
Sarah
Administrators
```

Used for user authentication.

---

### Computer Objects

```text
PC-01
PC-02
SERVER-01
```

Represent systems joined to the domain.

---

### Group Objects

Examples:

```text
Domain Users
Domain Admins
Help Desk
IT Team
```

Used to assign permissions to multiple users.

---

## Organizational Units (OU)

Organizational Units help organize objects.

Example:

```text
Company
│
├── HR
├── Finance
├── IT
└── Sales
```

Users and computers can be grouped into departments.

---

## Active Directory Authentication

When a user logs in:

```text
User
↓
Domain Controller
  ↓
Authentication
  ↓
Access Granted
```

The Domain Controller verifies the user's identity.
Modern Active Directory environments primarily use Kerberos for authentication.

---

## Group Policy (GPO)

Group Policy allows administrators to apply settings across multiple systems.

Examples:

- Password policies
- Desktop settings
- Security configurations
- Software deployment

Example:

```text
Password Length = 12 Characters
```

Applied to all users in the domain.

SOC Note:
Misconfigured Group Policies can introduce security risks.

---

## Common Active Directory Components

| Component| Purpose |
|----------|---------|
| Domain | Collection of users and computers |
| Domain Controller | Manage Active Directory |
| User Object | Represents a system |
| Computer Object | Represents a system |
| Group | Collections of users |
| OU | Organizational Unit |
| GPO | Group Policy Object |

---

## Why attackers target Active Directory?

Active Directory often contains:

- User accounts
- Administrator accounts
- Service accounts
- Group memberships
- Authentication data

Attack Goal:

```text
 Compromise User
        ↓
Privilege Escalation
        ↓
  Domain Admin
        ↓
Full Domain Control
```

SOC Note:
Compromise of Active Directory can impact the entire organization.

---

## Common Active Directory Attacks 

Examples:

- Credential Dumping
- Pass-the-Hash
- Kerberoasting
- Golden Ticket Attacks
- Privilege  Escalation
- Lateral Movement

---

## Detection Opportunities

Monitor for:

- Unusual logon activity
- New administrator accounts
- Group membership changes
- Privileged account usage
- Authentication anomalies
- Domain Controller access

---

## Important Event IDs

| Event ID | Description |
|----------|-------------|
| 4624 | Succcessful Logon |
| 4625 | Failed Logon |
| 4672 | Special Privileged Assigned |
| 4720 | User Account Created |
| 4728 | User Added to Security Group |
| 4732 | User Added to Local Group |

---

## Investigation Questions

When investigating Active Directory activity:

- Which account performed the action?
- Was a privileged account involved?
- Were group memberships modified?
- Was lateral movement observed?
- Was a Domain Controller accessed?

---

## Attack Scenario 

```text
Attacker Compromise User
           ↓
 Credential Dumping
            ↓
 Privilege Escalation
            ↓
 Domain Admin Access
            ↓
 Full Domain Control
```

---

## Quick Summary

| Term | Meaning |
|------|---------|
| Active Directory | Centralized identity management system |
| Domain | Collection of users and computers |
| Domain Controller | Server managing Active Directory |
| User Object | Represents a user account |
| Computer Object | Represents a system |
| Group | Collection of users with shared permissions |
| OU | Organizational Unit |
| GPO | Group Policy Object |

---

## What is Active Directory?

Active Directory is a centeralized directory service that manages 
users, computers, groups, authentication, and security policies within a Windows domain environment. 

