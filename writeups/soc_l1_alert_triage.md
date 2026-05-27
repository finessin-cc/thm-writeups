# TryHackMe: SOC L1 Alert Triage

- **Difficulty:** Easy
- **Date:** 2026-05-27
- **Platform:** TryHackMe

## 🎯 Description
Automated writeup skeleton for the **SOC L1 Alert Triage** room.

## 🔍 Phase 1: Reconnaissance (Nmap & Web Enumeration)
```bash
nmap -sC -sV -oN nmap/initial $(target_ip)
```
*Reviewing open ports and identifying potential entry points based on the room type.*

## 🚀 Phase 2: Exploitation / Initial Access
1. Identified vulnerable services or misconfigurations.
2. Executed relevant exploit or brute-force vector to gain a user shell.
3. Captured the user flag.

*User Flag:* `THM{REDACTED_USER_FLAG}`

## 👑 Phase 3: Privilege Escalation
* Checking `sudo -l` permissions.
* SUID binaries exploitation or kernel vulnerability check.
* Escalated privileges to root.

*Root Flag:* `THM{REDACTED_ROOT_FLAG}`

## 📝 Takeaways
* Always check for basic misconfigurations before trying complex exploits.
