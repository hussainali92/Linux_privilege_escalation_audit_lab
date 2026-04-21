# Linux Privilege Escalation Detection Lab with auditd and auth.log

## Overview
This lab simulates suspicious privilege escalation activity on Ubuntu.  
The scenario includes:
- creating a low-privileged user
- failed sudo attempts
- creating a new privileged administrative account
- adding that account to the sudo group
- logging in through SSH
- creating another user from the privileged account
- validating the activity through auth.log and auditd

## Lab Goals
- Detect failed and successful sudo activity
- Track user creation and group changes
- Monitor identity-related file changes
- Correlate SSH access with privilege escalation behavior
- Practice Linux log analysis using auth.log and ausearch

## Environment
- OS: Ubuntu 22.04
- Service 1: OpenSSH Server
- Service 2: auditd
- Log sources:
  - /var/log/auth.log
  - auditd / ausearch

## Attack Simulation Steps
1. Enabled SSH and auditd
2. Created low-privileged user `labuser`
3. Loaded custom auditd rules
4. Logged in as `labuser` via SSH
5. Attempted `sudo -l` and `sudo id` and confirmed failure
6. From the main administrative account, created `adminops`
7. Added `adminops` to the `sudo` group
8. Logged in as `adminops`
9. Verified `sudo` access with `sudo -l` and `sudo id`
10. Created another user named `tempops`
11. Reviewed evidence in auth.log and auditd

## Detection Commands Used

### Service verification
```bash
sudo systemctl status ssh --no-pager
sudo systemctl status auditd --no-pager
