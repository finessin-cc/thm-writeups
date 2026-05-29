# TryHackMe: SOC Metrics and Objectives

## Room Metadata
| Platform | Type | Difficulty | Date |
|----------|------|------------|------|
| TryHackMe | SOC | Easy | 2023-10-01 |

## Task 1: Introduction
No answer needed

## Task 2: Core Metrics
### Metrics
| Metric | Formula | Measures |
|--------|---------|----------|
| Alerts Count (AC) | AC = Total Count of Alerts Received | Overall load of SOC analysts |
| False Positive Rate (FPR) | FPR = False Positives / Total Alerts | Level of noise in the alerts |
| Alert Escalation Rate (AER) | AER = Escalated Alerts / Total Alerts | Experience of L1 analysts |
| Threat Detection Rate (TDR) | TDR = Detected Threats / Total Threats | Reliability of the SOC team |

### Questions
- **Is zero alerts for one month a good sign for your SOC team? (Yea/Nay)**  
  - **Answer**: Nay
- **What is the False Positive Rate if only 10 out of 50 alerts appear to be real threats?**  
  - **Answer**: 80%

## Task 3: Triage Metrics
### SLA Metrics
| Metric | Common SLA | Description |
|--------|------------|-------------|
| SOC Team Availability | 24/7 | Working schedule of the SOC team, often Monday-Friday (8/5) or 24/7 mode |
| Mean Time to Detect (MTTD) | 5 minutes | Average time between the attack and its detection by SOC tools |
| Mean Time to Acknowledge (MTTA) | 10 minutes | Average time for L1 analysts to start triage of the new alert |
| Mean Time to Respond (MTTR) | 60 minutes | Average time taken by SOC to actually stop the breach from spreading |

### Questions
- **Imagine a scenario where the SOC team receives a critical alert on Saturday. If the team works 8/5, on which day of the week will they acknowledge the alert?**  
  - **Answer**: Monday
- **Imagine a scenario where an employee was lured into running data stealer malware. The SOC team received the "Connection to Redline Stealer C2" alert after 12 minutes. One of the L1 analysts on shift moved the alert to In Progress 10 minutes later. After 6 minutes, the alert was escalated to L2, who spent 35 minutes cleaning the malware. Provide the MTTD, MTTA, and MTTR via comma as your answer (e.g. 10,20,30).**  
  - **Answer**: 12,10,51

## Task 4: Improving Metrics
### Recommendations
| Issue | Recommendations |
|-------|-----------------|
| False Positive Rate over 80% | 1. Exclude trusted activities like system updates from your EDR or SIEM detection rules 2. Consider automating alert triage for most common alerts using SOAR or custom scripts |
| Mean Time to Detect over 30 min | 1. Contact SOC engineers to make the detection rules run faster or with a higher rate 2. Check if SIEM logs are collected in real-time, without a 10-minute delay |
| Mean Time to Acknowledge over 30 min | 1. Ensure the analysts are notified in real-time when a new alert appears 2. Try to evenly distribute alerts in the queue between the analysts on shift |
| Mean Time to Respond over 4 hours | 1. As L1, make everything possible to quickly escalate the threats to L2 2. Ensure your team has documented what to do during different attack scenarios |

### Questions
- **What is the highest acceptable False Positive Rate for SOC teams?**  
  - **Answer**: 80%
- **Should all SOC roles work together to keep metrics improving? (Yea/Nay)**  
  - **Answer**: Yea

## Task 5: Practice Scenarios
### Practice
- **View Site**: For this lab, imagine yourself as a SOC manager receiving different complaints related to the SOC team. Open the attached site by clicking the View Site button and try to improve SOC metrics across three scenarios by correctly assigning improvement tasks from the list. Once completed, claim the flags and answer the task questions!

### Questions
- **What flag did you get after completing the first scenario?**  
  - **Answer**: THM{mttr:quick_start_but_slow_response}
- **What flag did you get after completing the second scenario?**  
  - **Answer**: THM{mttd:time_between_attack_and_alert}
- **What flag did you get after completing the third scenario?**  
  - **Answer**: THM{fpr:the_main_cause_of_l1_burnout}
