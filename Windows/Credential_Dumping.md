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

``` text
lsass.exe
```

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
SAM (Security Account Manager) is a Windows database that stores local user account information.

Location:

```text
C:\Windows\System32\Config\SAM
```

Contains:

- Local user accounts
- NTLM password hashes
- Security information for local users

SOC Note:
Attackers often attempt to access or copy the SAM database to obtain password hashes for offline cracking.

---

## NTDS.dit
NTDS.dit is the Active Directory database used on Domain Controllers.

Location:

```text
C:\Windows\NTDS\NTDS.dit
```

Contains:

- Domain user accounts
- Password hashes
- Group information
- Active Directory objects

SOC Note:
Unauthorized access to NTDS.dit is a critical security incident because it can expose credentials for an entire domain.

---

## Common Credential Dumping Tools

### Mimikatz
Mimikatz is one of the most widely used credential dumping tools.

Capabilities:

- Dump plaintext passwords
- Extract NTLM hashes
- Extract Kerberos tickets
- Perform Pass-the-Hash attacks

SOC Note:
Detection of Mimikatz is often treated as a high-confidence indicator of compromise.

---

### ProcDump

ProcDump is a legitimate Microsoft utility that attackers can abuse.

Example:

```cmd
procdump.exe -ma lsass.exe lsass.dmp
```

Purpose:

- Creates a memory dump of LSASS

SOC Note:
Unexpected ProcDump execution against LSASS should be investigated immediately.

---

## Indicators of Credential Dumping

Look for:

- Access to lsass.exe
- Creation of dump files
- Mimikatz execution
- ProcDump execution
- Suspicious PowerShell activity
- Unusual administrator behavior

Common dump files:

```text
lsass.dmp
memory.dmp
dump.bin
```

---

## Relevant Event IDs

| Event ID | Description |
|-----------|------------|
| 4688 | Process Creation |
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4672 | Special Privileges Assigned |
| 7045 | Service Installed |

---

## MITRE ATT&CK

| Technique | Name |
|------------|------|
| T1003 | OS Credential Dumping |

---

## Quick Summary

| Item | Purpose |
|--------|---------|
| LSASS | Stores authentication data |
| SAM | Local account hashes |
| NTDS.dit | Domain account database |
| Mimikatz | Credential dumping tool |
| ProcDump | Dumps process memory |
| 4688 | Process creation event |
| 4672 | Privileged account activity |

