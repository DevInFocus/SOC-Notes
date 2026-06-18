# Privilege Escalation (SOC Analyst Notes)

## Overview

Privilege Escalation is a technique used by attackers to gain higher permissions on a system after initial access.
The goal is to move from a low-privileged account to an account with greater privileges, such as Administrator, SYSTEM, or Domain Admin.

MITRE ATT&CK:
- T1068 - Exploitation for Privilege Escalation
- T1548 - Abuse Elevation control Mechanism

---

## Why attackers perform Privilege Escalation?

After compromising a system, attackers often have limited access to perform additional actions, they attempt to obtain elevated privileges.

Examples:

- Disable security tools
- Access sensitive files
- Dump credentials
- Create new accounts
- Move laterally through the network

Example Attack Path:

Initial Access
↓
Privilege Escalation
↓
Credential Dumping
↓
Lateral Movement
↓
Persistence

---

## Types of Privilege Escalation

### Vertical Privilege Escalation

A user gains higher privileges on the same system.

Example:

```text
User -> Administrator
```

SOC Note:
Most common form of privilege escalation.

---

### Horizontal Privilege Escalation

A user gains access to another account with similar privileges.

Example:

```text
UserA -> UserB
```

SOC Note:
Often achieved through credential theft.

---

## Common Privilege Levels in Windows

### Standard User

Permissions:

- Run applications
- Access personal files
- Limited system changes

SOC Note:

Most users should operate with standard privileges.

---

### Administrator

Permissions:

- Install software
- Modify system settings
- Manage user accounts

SOC Note:

Administrator accounts are frequent attacker targets.

---

### SYSTEM

Highest privilege level in Windows.

Account:

```text
NT Authority\SYSTEM
```

SOC Note:

Attackers obtaining SYSTEM access have nearly full control of the host.

---

## Common Privilege Escalation Techniques

### Expoliting Vulnerabilities

Attackers obtaining SYSTEM access have nearly full control of the host.

---

## Common Privilege Escalation Techniques

### Exploiting Vulnerabilities 

Attackers abuse software or operating system vulnerabilities.

Example:

- Unpatched Windows vulnerability
- Vulnerable application

---

SOC Note:

Regular patching reduces this risk 

---

### Weak Service Permissions

Misconfigured services can allow attackers to modify service binaries.

Example:

```text
Service executable is writable by normal users
```

SOC Note:

Can lead to SYSTEM-level execution.

---

### Unquoted Service Paths

Example:

```text
C:\Program Files\My Service\service.exe
```

Without quotes, Windows may execute an attacker-controlled file.

SOC Note:
Common Windows privilege escalation finding.

---

### Scheduled Tasks

Attackers abuse scheduled tasks running with elevated privileges.

SOC Note:
Review task ownership and permissions.

---

### Credential Reuse

Attackers obtain administartive credentials and log in as privileged users.

Examples:

- Password reuse
- Stolen credentials
- Pass-the-Hash

SOC Note:
Often follows credential dumping activity.

---

## Indicators of Privilege Escalation

Look for:

- New administrator accounts
- Unexpected privilege assignments
- Service modifications
- Scheduled task creation
- Security tool tampering
- Privileged logons from unusual users

---

## Relevant Event IDs

| Event ID | Description |
|----------|-------------|
|4624 | Successful Logon |
|4625 | Failed Logon |
|4672 | Special Privileged Assigned |
|4688 | Process Creation |
|4720 | User Account Created|
|4728 | User Added to Security Group |
|4732| User Added to Local Group |
|7045| Service Installed |

---

### Step 1

Identify privileged logons.

Check:

- Event ID 4624
- Event ID 4672


Questions:

- Who logged in?
- When?
- From where?

---

### Step 2

Review process creation activity.

Check:

```text
Event ID 4688
```

Look for:

- PowerShell
- cmd.exe
- rundll32.exe
- suspicious executables

---

### Step 3

Check for account modifications.

Review:

- New users
- Group membership changes
- Administrator additions

---

### Step 4

Review persistence mechanisms.

Look for:

- New services
- Scheduled tasks
- Startup entries

---

### Step 5

Determine impact.

Questions: 

- Was SYSTEM access obtained?
- Was credential dumping performed?
- Was lateral movement observed?

---

## Red Flags

- Standard user suddenly recieving admin rights
- Event ID 4672 from unusual accounts
- New administrator account creation
- Unexpected service installation
- Privileged activity outside business hours
- Multiple failed logons followed by success

---

## Detection Opportunities

Monitor:

- Privileged logons
- Group membership changes
- Process creation events
- Service creation events
- Scheduled task creation
- PowerShell activity


EDR alerts may detect:

- Token manipulation
- UAC bypass attempts
- Service abuse
- Privilege escaltion exploits

---

## Quick Summary

| Item | Purpose |
|------|---------|
| Standard User | Limited permissions |
| Administrator | Elevated permissions |
| SYSTEM | Highest local privilege |
| 4672| Special privileges assigned |
| 4688| Process creation |
| 4720 | User account created |
| 7045| Service installed |

---

## MITRE ATT&CK

| Technique | Name |
|------------|------|
| T1068 | Exploitation for Privilege Escalation |
| T1548 | Abuse Elevation Control Mechanism |

---

