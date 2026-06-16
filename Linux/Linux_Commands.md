#Linux Commands

## Navigation Commands

### pwd
Shows the current working directory.

SOC Use:
Identify where you are investigating. 

### ls
Lists files and directories.

SOC Use: 
View files and folders.

### ls -l
Displays detailed file information including permissions.

SOC Use:
Investigate file permsissions and ownership.

### cd
Changes directory.

SOC Use:
Navigate to logs and investigation folders.

---

## File Viewing Commands

### cat 
Displays file contents.

SOC Use:
Read logs and configuration files.

### tail
Displays the last lines of a file.

SOC Use:
View recent log activity.

### tail -f
Monitors a file in real time.

SOC Use:
Watch logs as new events occur.

---

## Search Commands

### grep
Searches for specific text patterns.

SOC Use:
Find failed logs, IP addresses, and suspicious events.

### find
Searches for files and directories.

SOC Use:
Locate logs and suspcious files.

---

## Process Commands

### ps aux

Displays running processes.

SOC Use:
Identify suspicious processes.

### top
Shows real-time process activity.

SOC Use:
Monitor system activity.

### Kill
Terminate a running process. Stop a process using its Process ID (PID) 
Kill PID

SOC Use:
Used to stop suspicious, malicious, or unncessary processes during an investigation.

---

## Network Commands

### netstat
Displays active network connections.

SOC Use:
Identify suspicious connections.

### ss
Displays network socket information.

SOC Use:
Investigate listening ports and connections.

---

## Key Learning 
Linux commands help SOC analysts navigate systems, analyze logs, monitor processes, and investigate security incidents.
