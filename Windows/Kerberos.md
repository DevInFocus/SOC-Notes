
# Kerberos Authentication

## Overview

Kerberos is the primary authentication protocol used in modern Windows Active Directory environments. 
It allows users to authenticate securely without repeatedly sending passwords across the network.

SOC Note: 
Kerberos is widely used in enterprise environments and is frequently targeted by attackers. 

---

## Why Kerberos exists?

Before kerberos, authentication often relied on password-based methods.

Problem:

```text
User
 ↓
Sends Credentials
 ↓
Server
```

This created security risks.

Kerberos improves security by using tickets instead of repeatedly transmitting credentials.

---

## Key Components

## User

The person attempting to access resources.

Example:

```text
shri
```

---

### Domain Controller (DC)

The server responsible for authentication. 

---

### KDC (Key Distribution Center)

The KDC runs on the Domain Controller.

Responsibilities:

- Verifies users
- Issues tickets
- Controls authentication

---

## Kerberos Authentication Process

### Step 1 : User Logs In

```text
Username
Password
```

The user's credential are verified.

---

### Step 2 : TGT Issued

TGT = Ticket Granting Ticket

```text
User
↓
Domain Controller
 ↓
TGT Issued
```

The TGT proves the user has successfully authenticated.

SOC Note:

The TGT is the user's "authentication passport."

---

### Step 3: Request Access

The user wants to access a resource.

Example:

```text
File Server
Database Server
Application Server
```

---

### Step 4: TGS Issued

TGS = Ticket Granting Service Ticket

```text
TGT
 ↓
KDC
 ↓
TGS
```

The user recieves a service ticket for the requested resource.

---

### Step 5 : Resource Access

```text
User
↓
Service Ticket
 ↓
Server
 ↓
Access Granted
```

The server verifies the ticket and grants access.

---

## Kerberos Workflow

```text
User Login
     ↓
TGT Issued
     ↓
User Requests Resource
     ↓
TGS Issued
     ↓
Access Granted
```

---

## Important Terms

### TGT (Ticket Granting Ticket)

Purpose:

```text
Proves User Identity
```

Obtained after successful login 

---

### TGS (Ticket Granting Service Ticket)

Purpose:

```text
Provides Access To A Service
```

Used when accessing resources.

### SPN (Service Principal Name)

Unique identifier for a service.

Examples:

```text
MSSQL
HTTP
CIFS
```

SOC Note:

SPNs are important in Keraberosting attacks.

---

## Kerberos Vs NTLM

| Feature | Kerberos | NTLM |
|---------|----------|------|
| Uses Tickets | Yes | No |
| Uses Domain Controller| Yes | Sometimes |
| Modern Authentication | Yes | Older Protocol |
| Preferred in AD | Yes | No |
| Common Attack Target | Yes | No |

---

Why attackers target Kerberos?

Kerberos provides access to important resources.

Attackers may attempt to:

- Steal tickets
- Forge tickets
- Escalate privileges
- Move laterally

---

## Common Kerberos Attacks

## Kerberoasting 

Attackers request service tickets and attempt to crack them offline.

Goal:

```text
Recover Service Account Passwords
```

---

### Golden Ticket Attack

Attacker creates a forged TGT.

Result:

```text
Near-Unlimited Domain Access
```

SOC Note:

One of the most serious Active Directory attacks.

Result:

```text
Access Specific Services
```

Without contacting the Domain Controller.

---

## Detection Opportunities

Monitor for:

- Unusual ticket requests
- Excessive Kerberos activity
- Service account abuse
- Privileged account activity
- Authentication anomalies

---

## Related Event IDs

| Event ID | Description |
|-----------|------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4768 | Kerberos Authentication Ticket Requested |
| 4769 | Kerberos Service Ticket Requested |
| 4771 | Kerberos Authentication Failure |

---

## Investigation Questions

When investigating Kerberos activity:

- Which account requested the ticket?
- Was the request normal?
- Was a service account involved?
- Were excessive ticket requesrs observed?
- Was privilege escalation attempted?

---

## Attack Scenario

```text
Attacker Compromises User
            ↓
Requests Kerberos Tickets
            ↓
Performs Kerberoasting
            ↓
Obtains Service Account Password
            ↓
Privilege Escalation
            ↓
Domain Compromise
```

---

## Quick Summary


| Term | Meaning |
|--------|---------|
| Kerberos | Authentication protocol used in Active Directory |
| KDC | Key Distribution Center |
| TGT | Ticket Granting Ticket |
| TGS | Service Ticket |
| SPN | Service Principal Name |
| Kerberoasting | Attack against service accounts |
| Golden Ticket | Forged TGT |
| Silver Ticket | Forged Service Ticket |

---

## SOC Interview Question

### What is the difference between NTLM and Kerberos?

NTLM uses password hashes for authentication, while Kerberos uses a ticket-based system. Kerberos is the preferred authentication protocol in modern Active Directory environments because it provides stronger security and reduces crendential exposure. 

