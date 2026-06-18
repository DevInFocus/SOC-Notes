# Credential Dumping 

## Overview

Credential Dumping is a technique used by attackers to extract usernames, passwords, hashes, and authentication tickets from a compromised system.

The goal is to obtain valid credentials that can be used for:

- Privilege Escalation
- Lateral Movement
- Persistence
- Access to sensitive resources

  Credential is a common technique observed during post-exploitation activities.

MITRE ATT&CK:
- T1003 - OS Credential Dumping

---

## Why attackers Dump Credentials

Attackers often gain access to a low-privileged account first.

To move further inside the network, they attempt to steal credentials from memory or security databases.

Example Attack Path:

1. Initial Access
2. Credential Dumping
3. Privilege Escalation
4. Lateral Movement
5. Domain Compromise

---

## Common Credential Sources

### LSASS Memory

LSASS (Local Security Authority Subsystem Service) stores authentication information in memory.

Process:

```text
lsass.exe

---

## What attackers target in LSASS?

Attackers target LSASS because it  may contain:

- Plaintext passwords
- NTLM password hashes
- Kerberos tickets
- Authentication tokens

SOC Note:
Unauthorized access to LSASS is highly suspicous and may indicate credential dumping activity.

---

## SAM Database









