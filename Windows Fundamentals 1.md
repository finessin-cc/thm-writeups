# TryHackMe: Windows Fundamentals 1

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | Windows Fundamentals        |
| Difficulty    | Beginner                    |
| Date          | Not specified               |

## Task 1: Windows Editions

Windows has evolved significantly since its inception in 1985, with each version introducing new features and improvements. Key points include:

- Windows XP was popular but eventually reached end-of-life
- Windows Vista was poorly received and quickly phased out
- Windows 7 became the preferred choice after XP's end-of-life
- Windows 8 was short-lived
- Windows 10 and Windows 11 are current desktop versions
- Windows Server 2025 is the current server version

**Question:** What encryption can you enable on Pro that you can't enable in Home?
- **Answer:** BitLocker

## Task 2: The Desktop (GUI)

The Windows Desktop provides a graphical user interface with several key components:

### Desktop Components
- **Desktop**: Contains shortcuts to programs, folders, and files
- **Start Menu**: Access to apps, programs, and system settings
- **Search Box (Cortana)**: Search functionality
- **Task View**: Virtual desktop management
- **Taskbar**: Shows running applications and system indicators
- **Notification Area**: Displays system icons like clock, network, and volume

### Start Menu Sections
1. **Account Actions**: User account settings, lock, sign out, documents, pictures, settings, power options
2. **All Apps**: Alphabetically organized list of installed applications
3. **Pinned Apps**: Frequently used applications as tiles

### Taskbar Features
- Shows running applications
- Provides previews and tooltips
- Allows pinning applications for quick access

### Notification Area
- Displays system icons including clock, network, volume
- Can be customized in Taskbar settings

**Questions:**
- Which selection will hide/disable the Search box?
  - **Answer:** Hidden
- Which selection will hide/disable the Task View button?
  - **Answer:** Show Task View button
- Besides Clock and Network, what other icon is visible in the Notification Area?
  - **Answer:** Action Center

## Task 3: Introduction to Windows

This task provides instructions for accessing the lab environment:

- Start the lab machine using the provided button
- Access via Remote Desktop using credentials:
  - Machine IP: MACHINE_IP
  - User: administrator
  - Password: letmein123!

**Note:** The lab machine may take up to 3 minutes to load.

## Task 4: The File System

Modern Windows uses the New Technology File System (NTFS) as its primary file system, replacing older systems like FAT16/FAT32 and HPFS.

### NTFS Features
- **Journaling capability**: Automatically repairs file system after failures
- **Supports files larger than 4GB**
- **Specific permissions on folders and files**
- **Folder and file compression**
- **Encryption (EFS)**

### NTFS Permissions
- Full control
- Modify
- Read & Execute
- List folder contents
- Read
- Write

### Alternate Data Streams (ADS)
- NTFS-specific feature allowing multiple data streams per file
- Used by malware for hiding data
- Not visible in Windows Explorer by default
- Can be viewed using PowerShell

**Question:** What is the meaning of NTFS?
- **Answer:** New Technology File System

## Task 5: The Windows\System32 Folders

The Windows folder (typically C:\Windows) contains the core operating system files.

### System32 Folder
- Contains critical system files
- Requires extreme caution when modifying
- Deleting files can render Windows inoperable
- Many essential tools reside in this folder

**Question:** What is the system variable for the Windows folder?
- **Answer:** `%windir%`

## Task 6: User Accounts, Profiles, and Permissions

### User Account Types
- **Administrator**: Can make system-wide changes
- **Standard User**: Limited to user-specific changes

### User Profiles
- Located in C:\Users
- Created upon first login
- Include standard folders (Desktop, Documents, Downloads, Music, Pictures)

### Local User and Group Management
- Accessed via `lusrmgr.msc`
- Manages users and groups
- Groups inherit permissions assigned to them
- Users can belong to multiple groups

**Questions:**
- What is the name of the other user account?
  - **Answer:** tryhackmebilly
- What groups is this user a member of?
  - **Answer:** Remote Desktop Users,Users
- What built-in account is for guest access to the computer?
  - **Answer:** Guest
- What is the account description?
  - **Answer:** window$Fun1!

## Task 7: User Account Control

User Account Control (UAC) protects systems by running administrator accounts with standard privileges by default.

### How UAC Works
- Administrator sessions run with standard privileges
- Elevated privileges required for system changes
- UAC prompts user confirmation for privileged operations
- Shield icons indicate UAC-enabled programs

**Question:** What does UAC mean?
- **Answer:** User Account Control

## Task 8: Settings and the Control Panel

### System Configuration Tools
- **Settings Menu**: Introduced in Windows 8, primary configuration location
- **Control Panel**: Traditional configuration interface for complex settings

### Access Methods
- Both accessible from Start Menu
- Settings is now primary location
- Control Panel handles more complex configurations
- Search function helps locate specific settings

### Installed Applications Management
- Control Panel → Programs → Programs and Features
- Lists all installed applications with versions and publishers

**Question:** In the Control Panel, change the view to Small icons. What is the last setting in the Control Panel view?
- **Answer:** Windows Defender Firewall

## Task 9: Task Manager

The Task Manager provides system monitoring and process management capabilities.

### Access Methods
- Right-click taskbar
- Keyboard shortcut: Ctrl+Shift+Esc

### Features
- Shows running applications and processes
- Displays CPU and RAM utilization
- Performance monitoring
- Process management capabilities

**Question:** What is the keyboard shortcut to open Task Manager?
- **Answer:** Ctrl+Shift+Esc
