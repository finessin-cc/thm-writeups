# TryHackMe: SOC L1 Alert Reporting

## Room Metadata
| Platform | Type | Difficulty | Date |
|----------|------|------------|------|
| TryHackMe | SOC | Easy | 2023-10-01 |

## Task 1: Introduction
No answer needed

## Task 2: Alert Funnel
### Alert Reporting
- **Alert Reporting**: Before closing or passing the alert to L2, you might have to report it. Depending on team standards and alert severity, instead of a short alert comment, you can be required to document your investigation in detail, ensuring all relevant evidence is included. This is especially important for True Positives, which require escalation.

### Alert Escalation
- **Alert Escalation**: If the True Positive alert requires additional actions or deeper investigation, escalate it to the L2 analyst for further review following the agreed procedures. That's where your alert report comes in handy since L2 will use it to get the initial context and spend less on the analysis from scratch.

### Communication
- **Communication**: You may also need to communicate with other departments during or after the analysis. For example, ask the IT team if they confirm granting administrative privileges to some users or contact HR to get more information about the newly hired employee.

### Questions
- **What is the process of passing suspicious alerts to an L2 analyst for review?**  
  - **Answer**: Alert Escalation
- **What is the process of formally describing alert details and findings?**  
  - **Answer**: Alert Reporting

## Task 3: Reporting Guide
### Alert Report Purpose
| Purpose | Explanation |
|---------|-------------|
| Provide context for escalation | A well-written report saves lots of time for L2 analysts and helps them quickly understand what happened |
| Save findings for the records | Raw SIEM logs are stored for 3-12 months, but alerts are kept indefinitely. It's better to keep all the context inside the alert, just in case |
| Improve investigation skills | If you can't explain it simply, you don't understand it well enough. Report writing is a great way to boost L1 skills by summarising alerts |

### Report Format
- **Who**: Which user logs in, runs the command, or downloads the file
- **What**: What exact action or event sequence was performed
- **When**: When exactly did the suspicious activity start and ended
- **Where**: Which device, IP, or website was involved in the alert
- **Why**: The most important W, the reasoning for your final verdict

### Questions
- **According to the SOC dashboard (opens in new tab), which user email leaked the sensitive document?**  
  - **Answer**: m.boslan@tryhackme.thm
- **Looking at the new alerts, who is the "sender" of the suspicious, likely phishing email?**  
  - **Answer**: support@microsoft.com
- **Open the phishing alert, read its details, and try to understand the activity. Using the Five Ws template, what flag did you receive after writing a good report?**  
  - **Answer**: THM{nice_attempt_faking_microsoft_support}

## Task 4: Escalation Guide
### Escalation Steps
- **Escalation**: After you have made a verdict and written your alert report, you must choose whether to escalate the alert to L2. You should escalate the alerts if:
  - The alert is an indicator of a major cyberattack requiring deeper investigation or DFIR
  - Remediation actions like malware removal, host isolation, or password reset are required
  - Communication with customers, partners, management, or law enforcement agencies is required
  - You just do not fully understand the alert and need some help from more senior analysts

### L1 Escalation Process
- **Escalation Steps**: To escalate the alert, in most cases, all you have to do is to reassign the alert to the L2 on shift and ping them in corporate chat or in person. In some teams, you may be required to create a formal written escalation request with dozens of required fields.

### SOC Dashboard Escalation
- **Move the alert to In Progress status and do the analysis**
- **Write an alert report and set your verdict, such as True Positive**
- **If escalation is required, assign the alert to your L2 on shift**
- **L2 will receive a notification and start from your alert report**

### Questions
- **Who is your current L2 in the SOC dashboard (opens in new tab) that you can assign (escalate) the alerts to?**  
  - **Answer**: E.Fleming
- **What flag did you receive after correctly escalating the alert from the previous task to L2?**  
  - **Answer**: THM{good_job_escalating_your_first_alert}

### Investigate the Second New Alert
- **Investigate the second new alert in the queue and provide a detailed alert comment.**
- **Decide if you need to escalate this alert and move on according to the process.**
- **After you finish your triage, you should receive a flag, which is your answer!**  
  - **Answer**: THM{looks_like_webshell_via_old_exchange}

## Task 5: SOC Communication
### Communication Cases
- **Critical Threat**: You need to escalate an urgent, critical alert, but L2 is unavailable and does not respond for 30 minutes. Ensure you know where to find emergency contacts. First, try to call L2, then L3, and finally your manager.
- **Slack/Teams Account Compromise**: The alert about Slack/Teams account compromise requires you to validate the login with the affected user. Do not contact the user through the breached chat - use alternative contact methods like a phone call.
- **Overwhelming Number of Alerts**: You receive an overwhelming number of alerts during a short period of time, some of which are critical. Prioritise the alerts according to the workflow, but inform your L2 on shift about the situation.
- **Misclassified Alert**: After a few days, you realise that you misclassified the alert and likely missed a malicious action. Immediately reach out to your L2 explaining your concerns. Threat actors can be silent for weeks before impact.
- **SIEM Logs Issues**: You can not complete the alert triage since the SIEM logs are not parsed correctly or are not searchable. Do not skip the alert - investigate what you can and report the issue to your L2 on shift or SOC engineer.

### Questions
- **Should you first try to contact your manager in case of a critical threat (Yea/Nay)?**  
  - **Answer**: Nay
- **Should you immediately contact your L2 if you think you missed the attack (Yea/Nay)?**  
  - **Answer**: Yea
