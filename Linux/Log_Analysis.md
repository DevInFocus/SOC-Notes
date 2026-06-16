# Log Analysis

## What is Log Analysis?
Log analysis is the process of examining log files identify system activity, security events, errors, and suspicious behavior.

## Why Logs matter?

Logs help analysts:

- Investigate security incidents
- Detects unauthorized access.
- Monitor system activity.
- Identify suspicious behavior

## Important Logs

### /var/log/auth.log

  Contains:

  - Sucessful logins
  - Failed login attempts
  - Authentication events
  - Privilege escalation activity
    
 ### /var/log/syslog

    Contains:

    - System events
    - Service activity
    - General system messages

 ## Common Commands

 - cat
 - grep
 - tail
 - tail -f

## What analysts look for?

- Failed login attempts
- Successful logins
- New user creation
- Privilege escalation
- Suspcious IP addresses
- Ununsual system activity

## Key Learning
Log analysis helps SOC analysts investigate security incidenrs and identify suspicious activity through system logs.
