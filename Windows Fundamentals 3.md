# TryHackMe: Windows Fundamentals 3

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | Windows Fundamentals        |
| Difficulty    | Beginner                    |
| Date          | Not specified               |

## Task 1: Introduction

Continues the Windows fundamentals series, focusing on security features within the Windows operating system. This module covers built-in Microsoft tools that help keep devices secure.

**Lab Access:**
- Machine IP: MACHINE_IP
- User: administrator
- Password: letmein123!

## Task 2: Windows Updates

Windows Update is Microsoft's service for providing security updates, feature enhancements, and patches for Windows and other Microsoft products.

### Key Points:
- Updates typically released on the 2nd Tuesday of each month (Patch Tuesday)
- Critical updates can be pushed immediately if urgent
- Updates can only be postponed, not indefinitely ignored (especially in Windows 10+)
- Requires reboot after installation

**Question:** There were two definition updates installed in the attached VM. On what date were these updates installed?
- **Answer:** 5/3/2021

## Task 3: Windows Security

Windows Security serves as the central hub for managing tools that protect the device and data.

### Protection Areas:
1. **Virus & threat protection**
2. **Firewall & network protection**
3. **App & browser control**
4. **Device security**

### Status Icons:
- **Green**: Device is sufficiently protected
- **Yellow**: Safety recommendations to review
- **Red**: Immediate attention needed

**Question:** Checking the Security section on your VM, which area needs immediate attention?
- **Answer:** Virus & threat protection

## Task 4: Virus & threat protection

### Current Threats:
- **Scan options**: Quick scan, Full scan, Custom scan
- **Threat history**: Last scan, Quarantined threats, Allowed threats

### Virus & Threat Protection Settings:
- **Real-time protection**: Locates and stops malware installation/execution
- **Cloud-delivered protection**: Enhanced protection with latest cloud data
- **Automatic sample submission**: Sends samples to Microsoft for threat protection
- **Controlled folder access**: Protects files from unauthorized changes
- **Exclusions**: Exclude specific files/folders from antivirus scanning
- **Notifications**: Alerts about security health and issues

### Ransomware Protection:
- Requires Controlled folder access to be enabled
- Real-time protection must be enabled (disabled in VM for performance reasons)

**Question:** Specifically, what is turned off that Windows is notifying you to turn on?
- **Answer:** Real-time protection

## Task 5: Firewall & network protection

### What is a Firewall?
Controls traffic flowing through ports, acting like a security guard checking IDs.

### Firewall Profiles:
- **Domain**: Used for authenticated domain networks
- **Private**: Used for home/private networks
- **Public**: Default for public networks (Wi-Fi hotspots, etc.)

### Security Recommendations:
- Keep Windows Defender Firewall enabled
- Configure app access through firewall
- Advanced settings for experienced users

**Question:** If you were connected to airport Wi-Fi, what most likely will be the active firewall profile?
- **Answer:** Public network

## Task 6: App & browser control

### Microsoft Defender SmartScreen:
- Protects against phishing/malware websites and applications
- Checks unrecognized apps and files from the web
- Can be set to Warn, Block, or Off

### Exploit Protection:
- Built into Windows 10/Server 2019
- Protects against attacks
- Default settings recommended for security

## Task 7: Device security

### Core Isolation:
- **Memory Integrity**: Prevents malicious code insertion into high-security processes

### Trusted Platform Module (TPM):
- Hardware component for security-related functions
- Secure crypto-processor with tamper-resistant mechanisms
- Works with BitLocker for enhanced protection

**Question:** What is the TPM?
- **Answer:** Trusted Platform Module

## Task 8: BitLocker

BitLocker Drive Encryption protects data from theft or exposure from lost/stolen devices.

### Key Features:
- Best protection when used with TPM version 1.2 or later
- TPM is a hardware component in many newer computers
- Works with BitLocker to protect user data and ensure system integrity

### Alternative for systems without TPM:
- Use removable drive containing startup key

**Question:** We should use a removable drive on systems without a TPM version 1.2 or later. What does this removable drive contain?
- **Answer:** startup key

## Task 9: Volume Shadow Copy Service

### What is VSS?
Volume Shadow Copy Service coordinates actions to create consistent shadow copies (snapshots) of data for backup purposes.

### Key Functions:
- Creates restore points
- Performs system restore
- Configures restore settings
- Deletes restore points

### Security Considerations:
- Malware writers often delete shadow copies to prevent ransomware recovery
- Requires offline/off-site backups for effective ransomware protection

**Question:** What is VSS?
- **Answer:** Volume Shadow Copy Service

## Summary

This final module in the Windows Fundamentals series covers essential security features including:
- Windows Update management
- Windows Security center and protection areas
- Virus and threat protection with real-time monitoring
- Firewall configuration for different network types
- App and browser control with SmartScreen
- Device security features including TPM and core isolation
- BitLocker encryption and startup key management
- Volume Shadow Copy Service for backup and recovery

These tools provide comprehensive protection for Windows systems and are essential knowledge for cybersecurity professionals working with Windows environments.
