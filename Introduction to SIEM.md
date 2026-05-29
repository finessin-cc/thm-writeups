# TryHackMe: Introduction to SIEM

## Room Metadata
| Platform | Type | Difficulty | Date |
|----------|------|------------|------|
| TryHackMe | SOC | Easy | 2023-10-01 |

## Task 1: Introduction
No answer needed

## Task 2: Logs Everywhere, Answers Nowhere
### Logs Everywhere
- **Network Diagram**: A network diagram showing multiple servers and workstations.

### Types of Log Sources
- **Host-Centric Log Sources**: Windows, Linux, servers, etc.
  - Examples: User accessing a file, user attempting to authenticate, process execution activity, PowerShell execution.
- **Network-Centric Log Sources**: Firewalls, IDS/IPS, routers, etc.
  - Examples: SSH connection, file being accessed via FTP, web traffic, user accessing company resources through VPN.

### Answers Nowhere
- **Registry-related activity**: host-centric
- **VPN-related activity**: network-centric

## Task 3: Why SIEM?
### SIEM Features
- **Centralized Log Collection**: SIEM collects logs from all sources (endpoints, servers, firewalls, etc.) and centralizes them in one place.
- **Normalization of Logs**: SIEM ensures all logs are broken down into different fields and presented in one consistent format.
- **Correlation of Logs**: SIEM correlates logs from different sources to identify malicious activities.
- **Real-time Alerting**: SIEM detects malicious activities based on detection rules and triggers alerts.
- **Dashboards and Reporting**: SIEM presents the data for analysis and provides actionable insights through dashboards.

## Task 4: Log Sources and Ingestion
### Log Sources
- **Windows Machine**: Logs are stored in the Event Viewer.
- **Linux Machine**: Logs are stored in various locations such as:
  - `/var/log/httpd`: HTTP Request/Response and error logs.
  - `/var/log/cron`: Events related to cron jobs.
  - `/var/log/auth.log` and `/var/log/secure`: Authentication-related logs.
  - `/var/log/kern`: Kernel-related events.

### Sample Logs
- **Cron Logs**:
  ```
  May 28 13:04:20 ebr crond[2843]: /usr/sbin/crond 4.4 dillon's cron daemon, started with loglevel notice
  May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-hourly)
  May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-daily)
  May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-weekly)
  May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-monthly)
  Jun 13 07:46:22 ebr crond[3592]: unable to exec /usr/sbin/sendmail: cron output for user root job sys-daily to /dev/null
  ```

- **Apache Logs**:
  ```
  192.168.21.200 - - [21/March/2022:10:17:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36"
  127.0.0.1 - - [21/March/2022:10:22:04 -0300] "GET / HTTP/1.0" 200 2216 "-" "curl/7.68.0"
  ```

### Log Ingestion
- **Agent / Forwarder**: Lightweight tool installed on endpoints to capture and send logs to the SIEM server.
- **Syslog**: Protocol to collect data from various systems and send it to a centralized destination.
- **Manual Upload**: Users can ingest offline data for quick analysis.
- **Port-Forwarding**: SIEM solutions can listen on a port, and endpoints forward data to the SIEM instance.

## Task 5: Alerting Process and Analysis
### Detection Rules
- **Examples**:
  - If a user gets five failed login attempts in 10 seconds, raise an alert for Multiple Failed Login Attempts.
  - If login is successful after multiple failed login attempts, raise an alert for Successful Login After Multiple Login Attempts.
  - If a user plugs in a USB, raise an alert (if USB is restricted).
  - If outbound traffic is > 25 MB, raise an alert for potential data exfiltration.

### Use-Case 1: Event Log Cleared
- **Rule**: If the Log source is WinEventLog AND EventID is 104 - Trigger an alert Event Log Cleared.

### Use-Case 2: WHOAMI Command Execution
- **Rule**: If Log Source is WinEventLog AND EventCode is 4688, and NewProcessName contains whoami, then Trigger an ALERT WHOAMI command Execution DETECTED.

## Task 6: Lab Work
### Lab Instructions
- **View Site**: Click on the View Site button to display the lab on the right side of the screen.

### Questions
- **After clicking on the Start Suspicious Activity button, which process caused the alert?**
  - **Answer**: cudominer.exe
- **Find the event that caused the alert and identify the user responsible for the process execution.**
  - **Answer**: chris
- **What is the hostname of the suspect user?**
  - **Answer**: HR_02
- **Examine the rule and the suspicious process; which term matched the rule that caused the alert?**
  - **Answer**: miner
- **Which option best represents the event? Choose from the following:**
  - **Answer**: True Positive
- **Selecting the right ACTION will display the FLAG. What is the FLAG?**
  - **Answer**: THM{000_SIEM_INTRO}
