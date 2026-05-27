# TryHackMe: SOC Alert Triage

## Room Metadata
| Platform | Type | Difficulty | Date |
|----------|------|------------|------|
| TryHackMe | SOC | Easy | 2023-10-01 |

## Task 1: Introduction
No answer needed

## Task 2: Events and Alerts
### Alert Management Platforms
| Solution | Examples | Description |
|----------|----------|-------------|
| SIEM | Splunk ES, Elastic | SIEM have solid alert management capabilities and are a perfect choice for most SOC teams |
| EDR or NDR | MS Defender, CrowdStrike | While EDR and NDR provide their own alert dashboards, it is preferred to use SIEM or SOAR |
| SOAR | Splunk SOAR, Cortex SOAR | Bigger SOC teams can use SOAR to aggregate and centralise alerts from multiple solutions |
| ITSM | Jira, TheHive | Some teams may have a custom ticket management (ITSM) setup using a dedicated solution |

### L1 Role in Alert Triage
- **SOC L1 analysts**: Review the alerts, distinguish bad from good, and notify L2 analysts in case of a real threat
- **SOC L2 analysts**: Receive the alerts escalated by L1 analysts and perform deeper analysis and remediation
- **SOC engineers**: Ensure the alerts contain enough information required for efficient alert triage
- **SOC manager**: Track speed and quality of alert triage to ensure that real attacks won't be missed

## Task 3: Alert Properties
### Alert Properties
| № | Property | Description | Examples |
|---|----------|-------------|----------|
| 1 | Alert Time | Shows alert creation time. Alert usually triggers a few minutes after the actual event | Alert Time: March 21, 15:35, Event Time: March 21, 15:32 |
| 2 | Alert Name | Provides a summary of what happened, based on the detection rule's name | Unusual Login Location, Email Marked as Phishing, Windows RDP Bruteforce, Potential Data Exfiltration |
| 3 | Alert Severity | Defines the urgency of the alert, initially set by detection engineers, but can be altered by analysts if needed | (🟢) Low / Informational, (🟡) Medium / Moderate, (🟠) High / Severe, (🔴) Critical / Urgent |
| 4 | Alert Status | Informs if somebody is working on the alert or if the triage is done | (🆕) New / Unassigned, (🔄) In Progress / Pending, (✅) Closed / Resolved |
| 5 | Alert Verdict | Also called alert classification, explains if the alert is a real threat or noise | (🔴) True Positive / Real Threat, (🟢) False Positive / No Threat |
| 6 | Alert Assignee | Shows the analyst that was assigned or assigned themselves to review the alert | Assignee can sometimes be called alert owner, Assignee takes responsibility for their alerts |
| 7 | Alert Description | Explains what the alert is about, usually in three sections on the right | The logic of the alert generating rule, Why this activity can indicate an attack, Optionally, how to triage this alert |
| 8 | Alert Fields | Provides SOC analysts' comments and values on which the alert was triggered | Affected Hostname, Entered Commandline, And many more, depending on the alert |

### Questions
- **What was the verdict for the "Unusual VPN Login Location" alert?**  
  - **Answer**: False Positive
- **What user was mentioned in the "Unusual VPN Login Location" alert?**  
  - **Answer**: M.Clark

## Task 4: Alert Prioritisation
### Picking the Right Alert
- **Filter the alerts**: Make sure you don't take the alert that other analysts have already reviewed, or that is already being investigated by one of your teammates.
- **Sort by severity**: Start with critical alerts, then high, medium, and finally low.
- **Sort by time**: Start with the oldest alerts and end with the newest ones.

### Questions
- **Should you first prioritise medium over low severity alerts? (Yea/Nay)**  
  - **Answer**: Yea
- **Should you first take the newest alerts and then the older ones? (Yea/Nay)**  
  - **Answer**: Nay

### Selected Alert
- **Name of the selected alert**: Potential Data Exfiltration

## Task 5: Alert Triage
### Initial Actions
- **Assign the alert to yourself**: Move it to In Progress.
- **Familiarise yourself with the alert details**: Name, description, and key indicators.

### Investigation
- **Understand who is under threat**: Affected user, hostname, cloud, network, or website.
- **Note the action described in the alert**: Suspicious login, malware, or phishing.
- **Review surrounding events**: Look for suspicious actions shortly after or before the alert.
- **Use threat intelligence platforms or other available resources**: Verify your thoughts.

### Final Actions
- **Decide if the alert is malicious (True Positive) or not (False Positive)**.
- **Prepare a detailed comment**: Explain your analysis steps and verdict reasoning.
- **Return to the dashboard and move it to the Closed status**.

### SOC Dashboard Notes
- If you didn't receive a flag after your triage, it means that the values you set are wrong.
- You can reset the SOC dashboard by clicking Restart on the top right in the TryHackMe SIEM.

### Flags
- **First-priority alert**: THM{looks_like_lots_of_zoom_meetings}
- **Second-priority alert**: THM{how_could_this_user_fall_for_it?}
- **Third-priority alert**: THM{should_we_allow_github_for_devs?}
