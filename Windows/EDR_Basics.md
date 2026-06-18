# EDR Basics 

## Overview

EDR (Endpoint Detection and Response) is a security solution that monitors endpoint activity, detects suspicious behavior, and helps security teams investigate and respond to threats.

Endpoints include:

- Windows computers
- Servers
- Laptops
- Virtual machines

Unlike traditional antivirus, EDR focuses on detecting malicious behavior rather than relying on known signatures.

---

## Why EDR is important?

Attackers often use legitimate tools and processes that may not be detected by antivirus software.

EDR helps analysts:

- Detect threats
- Investigate incidents
- Monitor endpoint activity
- Contain compromised systems
- Collect forensic evidence

SOC Note:
EDR is one of the primary tools used by SOC analysts during investigations.

---

## How EDR works?

EDR agents are installed on endpoints.

The agent collects:

- Process activity
- File activity
- Network connections
- User logins
- Registry changes
- Command-line activity

This information is sent to a central console where analysts can investigate alerts.

---

## Common EDR Capabilties

### Threat Detection

Identifies suspicious or malicious behavior.

Examples:

- Credential dumping
- Privilege escalation
- Malware execution
- Ransomware activity

---

### Process Monitoring 

Tracks process creation and execution.

Example:

```text
explorer.exe
└── cmd.exe
      └── powershell.exe
```

SOC Note:
Process relationships help identify malicious activity.

---

### File Monitoring

Monitors:

- File creation
- File Modification
- File deletion

Examples:

- Malware dropped on disk
- Suspicious executable creation

---

### Network Monitoring

Tracks:

- Outbound connections
- Inbound connections
- Communications with external IP addresses

SOC Note:
Useful for identifying Command and Control (C2) traffic.

---

### Endpoint Isolation

Allows analysts to isolate an infected system from the network.

Purpose

- Stop malware spread
- Prevent lateral movement
- Preserve evidence

SOC Note:
Common containment action during incidents.

---

## Important EDR Artifacts

### Process Tree

Shows parent-child process relationships.

Example:

```text
explorer.exe
  └── cmd.exe
      └── powershell.exe
```

SOC Note: 
One of the most important investigation tools in EDR.

---

### Command Line Activity

Example:

```text
powershell.exe - EncodedCommand
```

SOC Note:
Attackers frequently abuse PowerShell.

---

### User Activity

Tracks:

- Logons
- Logoffs
- Account usage

Usage for:

- Insider threat investigation
- Compromised account investigations

---

### Files Hashes

Unique identifiers for files.

Common types:

- MDS
- SHA1
- SHA256

SOC Note:
Used to identify known malicious files.

---

## Common EDR Alerts

### Credential Dumping

Indicators:

- Access to lsass.exe
- Mimikatz activity
- Memory dump creation

---

### Privilege Escalation

Indicators:

- New administrator accounts
- Special privilges assigned
- Service abuse

---

### Suspicious PowerShell

Indicators:

- Encoded commands
- Download commands
- Obfuscated scripts

---

### Malware Execution

Indicators:

- Suspicious executable launched
- Unknown file behavior
- Process injection activity

 ---

 ## Investigation Workflow

 ### Step 1

 Review alert details.

 Questions:

 - What triggered the alert?
 - Which host is affected?

---

### Step 2

Review process tree.

Look for:

- Parent process
- Child process
- Suspicious execution chain

---

### Step 3

Review command-line activity

Questions:

- What command was executed?
- Is it normal for the user?

---

### Step 4

Review network activity.

Check:

- External connections
- Suspicious IP addresses
- Command and Control communication

---

### Step 5

Determine impact.

Questions:

- Was malware executed?
- Were credentials accessed?
- Was lateral movement attempted?

---

## Response Actions

























