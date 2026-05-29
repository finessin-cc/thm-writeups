# TryHackMe: Snapped Phish-ing Line

## Room Metadata
| Platform | Type | Difficulty | Date |
|----------|------|------------|------|
| TryHackMe | SOC | Easy | 2023-10-01 |

## Task 1: A Series of Suspicious Emails
### Objectives
- Analyze the provided email samples to identify key artifacts.
- Investigate phishing URLs to understand redirection.
- Retrieve and examine the phishing kit used in the attack.
- Use CTI tools to gather intelligence on the adversary.
- Analyze the phishing kit to uncover additional indicators.

### Prerequisites
- Complete the previous four rooms of the Phishing Analysis Module:
  - Phishing Analysis Fundamentals
  - Phishing Emails in Action
  - Phishing Analysis Tools
  - Phishing Prevention

### Lab Access
- **Start Machine**: Click the Start Machine button to deploy the virtual machine.
- **Navigate to the desktop and open the phish-emails folder** to begin your investigation.

## Task 2: Email Analysis
### Questions
- **Which individual received the email regarding a Quote for Services Rendered?**
  - **Answer**: William McClean
- **What email address was used by the adversary to send the phishing emails?**
  - **Answer**: Accounts.Payable@groupmarketingonline.icu
- **Investigate the attachment in the email addressed to Zoe Duncan. What is the root domain of the redirection URL found within the file?**
  - **Answer**: kennaroads.buzz
- **Open the attachment in your VM web browser. Which company is the login page impersonating?**
  - **Answer**: Microsoft
- **Let’s check if the attacker left any files exposed on the same website. Navigate to the /data directory. What is the name of the archive file?**
  - **Answer**: Update365.zip
- **Download the phishing kit archive to your virtual environment. Using the sha256sum command, what is the SHA256 hash of the file?**
  - **Answer**: ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686
- **Investigate the file hash from the previous question using VirusTotal. Aside from phishing, what other threat category is assigned to the ZIP archive?**
  - **Answer**: Trojan
- **Review the VirusTotal Details page for the phishing kit. How many files are contained within the archive?**
  - **Answer**: 49
- **Let’s see if the attacker has exposed any captured credentials. Navigate to the /data/Update365/ directory and investigate the log file. What is the email address of the user who submitted their credentials more than once?**
  - **Answer**: michael.ascot@swiftspend.finance
- **Extract the phishing kit archive and locate the submit.php file. What email address is used by the adversary to collect compromised credentials?**
  - **Answer**: m3npat@yandex.com
- **Return to the phishing URL and locate the flag.txt file. Using CyberChef to decode the flag, what is the secret value?**
  - **Answer**: THM{pL4y_w1Th_tH3_URL}

## Task 3: Phishing Kit Analysis
### Phishing Kit Analysis
- **Phishing Kit**: The phishing kit used in the attack is a ZIP archive named `Update365.zip`.
- **SHA256 Hash**: The SHA256 hash of the file is `ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686`.
- **Threat Category**: The ZIP archive is categorized as a Trojan.
- **Files in the Archive**: The archive contains 49 files.
- **Captured Credentials**: The log file in the `/data/Update365/` directory shows that the email address `michael.ascot@swiftspend.finance` submitted their credentials more than once.
- **Credential Collection Email**: The adversary uses the email address `m3npat@yandex.com` to collect compromised credentials.

## Task 4: Phishing URL Investigation
### Phishing URL
- **Phishing URL**: The phishing URL used in the attack is `https://kennaroads.buzz/`.
- **Redirection**: The URL redirects to a Microsoft login page, impersonating Microsoft.

## Task 5: Intelligence Gathering
### CTI Tools
- **VirusTotal**: Used to gather intelligence on the phishing kit and identify additional indicators of compromise.
- **CyberChef**: Used to decode the flag from the `flag.txt` file.

## Task 6: Summary
- **Key Artifacts**: Email samples, phishing URLs, and the phishing kit.
- **Redirection**: The phishing URL redirects to a Microsoft login page.
- **Phishing Kit**: Contains 49 files and is categorized as a Trojan.
- **Captured Credentials**: The email address `michael.ascot@swiftspend.finance` submitted their credentials more than once.
- **Credential Collection Email**: The adversary uses the email address `m3npat@yandex.com` to collect compromised credentials.
- **Flag**: The secret value from the `flag.txt` file is `THM{pL4y_w1Th_tH3_URL}`.

## Task 7: Conclusion
- **Conclusion**: The phishing campaign was successful in compromising multiple employees at SwiftSpend Financial. The attacker used a combination of social engineering and technical means to gather credentials and potentially exfiltrate sensitive information.
- **Recommendations**: Implement stronger phishing awareness training, use multi-factor authentication, and regularly update security measures to prevent such attacks in the future.

## Task 8: Flag
- **Flag**: THM{pL4y_w1Th_tH3_URL}
