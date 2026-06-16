# Linux Fundamentals

## What is Linux?
Linux is an open-source operating system widely used in servers, cloud environments, and cybersecurity.

---

## Why Linux matters in  Cybersecurity
Many web servers, cloud systems, and security tools run on Linux. Security analysts often use Linux for investigations, log analysis, and system monitoring.

---

### Linux File System

Important directories:

- /home -> User directories
- /etc -> Configuration files
- /var -> Logs and variabl data
- /tmp -> Temporary files
- /root -> Root user directory

---
## Users and Groups

Linux uses users and groups to control access to files and system resources.

Examples:

- Regular User
- Root User
- Groups
- 
  ---

  ## File Permissions

  Linux permissions determine who can access files.

  ### Permission Types:

  - r = (Read) = 4
  - w = (Write) = 2
  - x = (Execute) = 1

  Example:

. 7 = rwx (4+2+1)
. 6 = rw- (4+2)
. 5 = r-x (4+1)
. 4 = r-- (4)

Example Permission

-rwxr-xr-x
### Equivalent Numeric Permission

755

Owner = rwx(7)
Group = r-x(5)
Others = r-x (5)

---

## Process Management
A process is a running program.

Common commands:

-ps
-top
-kill

---

## Log Files
Logs record system activity and are important during investigations.

Common logs:

-/var/log/auth.log
-/var/log/syslog

## Networking Commands

Userful commands:

-ping
-traceroute
-netstate
-ss

---

## Key Takeaway

Linux is a critical skill for SOC analysts because it helps in log analysis, process monitoring, user management, and security investigations.




















  
