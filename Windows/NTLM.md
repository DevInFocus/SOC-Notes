# NTLM (NT LAN Manager)

## Overview

NTLM (NT LAN Manager) is a Windows authentication protocol used to verify a user's identity. It allows Windows to confirm that a user knows the correct password without sending the actual password across the network. 

SOC Note:

Although Kerberos is the preferred authentication method in modern Active Directory environments, NTLM is still widely used and frequently abused by attackers.

---

## Why authentication is needed?

When a user logs in, Windows must verify their identity.

Example:

```text
Username: Defne
Password: Password123
```

Windows must determine whether the password is correct.

---

## Password vs Hash

Windows does not normally store passwords in plaintext.

Instead:

```text
Password
   ↓
Hash Function
   ↓
NTLM Hash
```

Example:

```text
Password123
↓
NTLM Hash
```

A hash is a mathematical representation of a password.

SOC Note:

Attackers often target hashes because they can sometimes be reused without knowing the actual password.

---

## How NTLM authentication works?

### Step 1

User enters username and password.

```text
User
↓
Username + Password
```

---

### Step 2

Windows creates an NTLM hash from the password.

```text
Password
↓
NTLM Hash
```

---

### Step 3

The generated hash is compared with the stored hash.

```text
Entered Hash
↓
Stored Hash
```

---

### Step 4
If both hashes match:

```text
Access Granted
```

If they do not match:

```text
Access Denied
```

---

## Why NTLM matters in SOC?
NTLM hashes are valuable targets for attackers.

If an attacker obtains a hash, they may attempt to:

- Reuse the hash
- Move laterally
- Gain Additional access
- Escalate privileges

---

## NTLM and Credential Dumping

Credential dumping tools often target NTLM hashes.

Example:

```text
LSASS
↓
NTLM Hashes
↓
Attacker Access
```

Common tools:

- Mimikatz
- ProcDump
- Credential dumping malware

SOC Note:
Credential dumping frequently aims to obtain NTLM hashes.

---

## Pass-the-Hash Attack

Pass-the Hash is a technique where attackers use a stolen NTLM hash instead of the actual password. 

Example:

```text
Attacker Steals Hash
↓
Uses Hash
↓
Authentication Succeeds
```

The attacker never needs to know the real password.

SOC Note:

Pass-the-Hash is one of the most common NTLM-related attack techniques.

---

## NTLM vs Kerberos

| Feature | NTLM | Kerberos|
|---------|------|---------|
| Older Protocol | Yes | No |
| Uses Password Hashes | Yes| No |
| Uses Tickets | No | Yes |
| Preferred in Modern Domains | No | Yes|
| Common Attack Target | Yes | Yes | 

---

## NTLM Weaknesses

Common weaknesses include:

- Pass-the-Hash attacks
- Relay attacks
- Credential theft
- Legacy protocol usage

SOC Note:
Organizations attempt to reduce NTLM usage whenever possible.

---

## Detection Opportunities

Monitor for:

- Credential dumping activity
- LSASS access
- Lateral movement
- Unusual authentication attempts
- Repeated logon activity

---

## Related Event IDs

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4672 | Special Privileges Assigned |
| 4688 | Process Creation |

---

## Investigation Questions

When investigating authentication activity:

- Was NTLM used?
- Were credentials dumped?
- Was LSASS accessed?
- Was Pass-the-Hash observed?
- Did lateral movement occur?

---

## Attack Scenario

```text
User Logs In
↓
NTLM Hash Stored
↓
Attacker Dumps Credentials
↓
Hash Stolen
↓
Pass-the-Hash Attack
↓
Access to Another System
```

---

## Quick Summary

| Term | Meaning |
|------|---------|
| NTLM | Windows authentication protocol |
| Hash | Mathematical representation of a password |
| Authentication | Identity verification process |
| LSASS | Stores authentication-related data |
| Pass-the-Hash | Using a stolen hash instead of a password |
| Credential Dumping | Stealing hashes or credentials |

---

### What is Pass-the-Hash?

Pass-the-Hash is an attack technique where an attacker authenticates using a stolen NTLM hash instead of the user's actual password. This allows access to systems without knowing the original password. 


