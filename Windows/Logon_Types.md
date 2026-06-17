# Logon Types in Windows (SOC Analysis Notes)

## Overview
In Windows systems, every login attempt is recorded with a logon Type. These values help SOC analysts understand how a user or attacker accessed a system.

Log data is mainly collected in:
- Microsoft Windows Event Viewer -> Security Logs

  Key Event IDs:
  - 4624 -> Successful logon
  - 4625 -> Failed logon
  - 4634 -> Logoff
  - 4648 -> Logon using explicit credentials

## Logon Type Breakdown

### Type 2 - Interactive Logon
Direct login at the system (keyboard or local access)

- Physical access to machine
- Standard desktop login

Use case:
User logging into office laptop

SOC insight:

- Normal activity on endpoints
- Suspicious on servers

---

### Type 3 - Network Logon
Access via network to shared resources

- File shares (SMB)
- Printer access
- Mapped drives

Use case:
- Accessing `\\server\share`

SOC insight:
- Common in lateral movement attacks
- Important for tracking credential resuse

---

### Type 4 - Batch Logon
Automated job execution

- Task Scheduler jobs
- Scripts running on schedule

Use case: 
- Backup scripts, system tasks

SOC insight:
Attackers may use for persistence

---

### Type 5 - Service Logon
Used by Windows services

- Background services
- Automatic startup processes

Use case: - 
Antivirus service, database service

SOC insight: 
- Malware may itself as a service


---

### Type 7 - Unlock
Session unlock event

- User resumes locked session

SOC insight:
- Normal behavior
- Unusual unlock times may be suspicious

---

### Type 8 - NetworkCleartext
Network logon using plaintext credentials

- Legacy authentication
- Rare in modern environments

SOC insight:
- High risk indicator
- May suggest insecure protocol usage

---

### Type 9 - NewCredentials
RunAs or alternate credentials used

- Executing process with different user

Example:
- runas /user:admin

SOC insight: 
- Possible privilege escalation technique

---

### Type 10 - RemoteInteractive (RDP)
Remote Desktopp login

- Full remote session
- One of the most critical logon types

Use case:
- Admin accessing server remotely

SOC insight:
- High attacker interest
- Brute force + credential stuffing target

---

### Type 11 - CachedInteractive
Offline login using cached credentials

- No domain controller required
- Used when system is offline

SOC insight:
- Normal for laptops
- Risk if device is stolen

---

## SOC Detection Tips

Always correlate:
- Logon Type
- IP Address
- Username
- Time of access
- Event IDs (4624 / 4625)

### Red Flags
- Multiple failed logins followed by success
- Type 3 -> Type 10 movement pattern
- Logins at unusual hours
- Servive accounts used interactively

---

## Quick Reference 

| Type | Meaning |
|------|---------|
| 2 | Local login |
| 3 | Network access |
| 4 | Batch job |
| 5| Service |
| 7 | Unlock session |
| 8 | Cleartext network login|
| 9 | RunAs / alternate creds|
| 10 | Remote Desktop (RDP) |
| 11 | Cached login |



  










  









