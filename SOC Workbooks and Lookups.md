# TryHackMe: SOC Workbooks and Lookups

## Room Metadata
| Platform | Type | Difficulty | Date |
|----------|------|------------|------|
| TryHackMe | SOC | Easy | 2023-10-01 |

## Task 1: Introduction
No answer needed

## Task 2: Assets & Identities
### Identity Inventory
- **Identity Inventory**: A catalogue of corporate employees (user accounts), services (machine accounts), and their details like privileges, contacts, and roles within the company. It helps in getting context about users and making decisions on expected activities.

### Asset Inventory
- **Asset Inventory**: A list of all computing resources within an organisation's IT environment. It is also called asset lookup and is used to get context about servers and workstations.

### Questions
- **Looking at the identity inventory, what is the role of R.Lund at the company?**  
  - **Answer**: US Financial Adviser
- **Checking the asset inventory, what data does the HQ-FINFS-02 server store?**  
  - **Answer**: Financial records
- **Finally, does the file sharing from the scenario look legitimate and expected? (Yea/Nay)**  
  - **Answer**: Yea

## Task 3: Network Diagrams
### Network Diagrams
- **Network Diagrams**: A visual schema presenting existing locations, subnets, and their connections. They help SOC analysts understand suspicious network activity.

### Questions
- **According to the network diagram, which service is exposed on the TCP/10443 port?**  
  - **Answer**: VPN
- **Now, which subnet would the server behind 172.16.15.99 IP belong to?**  
  - **Answer**: Database subnet
- **Finally, does the scenario look like a True Positive (TP) or False Positive (FP)?**  
  - **Answer**: TP

## Task 4: Workbooks Theory
### SOC Workbooks
- **SOC Workbooks**: Structured documents that define the steps required to investigate and remediate specific threats efficiently and consistently. They are used to support L1 analysts in triaging alerts.

### Workbook Example
- **Unusual Login Location Workbook**: A flowchart showing the process from receiving a login alert through identity enrichment via BambooHR, Threat Intel usage, investigation using Splunk, and escalation stages.

### Questions
- **Which SOC role would use workbooks the most (e.g. SOC Manager)?**  
  - **Answer**: SOC L1 Analyst
- **What is the process of gathering user, host, or IP context using TI and lookups?**  
  - **Answer**: Enrichment
- **Looking at the workbook example, what platform is used as an identity inventory source?**  
  - **Answer**: BambooHR

## Task 5: Workbooks Practice
### Practice
- **View Site**: Open the attached site by pressing the View Site button above and fill in the missing workbook steps from the options. Drag and drop the options to their respective positions. If the position is correct, the option will stick there. Once you are done, receive the flag and continue to the next section!

### Questions
- **What flag did you receive after completing the first workbook?**  
  - **Answer**: THM{the_most_common_soc_workbook}
- **What flag did you receive after completing the second workbook?**  
  - **Answer**: THM{be_vigilant_with_powershell}
- **What flag did you receive after completing the third workbook?**  
  - **Answer**: THM{asset_inventory_is_essential}
