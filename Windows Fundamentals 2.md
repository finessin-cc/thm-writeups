# TryHackMe: Windows Fundamentals 2

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | Windows Fundamentals        |
| Difficulty    | Beginner                    |
| Date          | Not specified               |

## Task 1: Introduction

Continues the exploration of the Windows operating system, building upon concepts from Windows Fundamentals 1. This module covers additional utilities and methods to access system configuration tools.

**Lab Access:**
- Machine IP: MACHINE_IP
- User: administrator
- Password: letmein123!

## Task 2: System Configuration and Advanced System Settings

### System Configuration (MSConfig)
The System Configuration utility (MSConfig) is for advanced troubleshooting with five main tabs:

1. **General**: Select boot options (Normal, Diagnostic, Selective)
2. **Boot**: Define boot options for the OS
3. **Services**: Lists all system services regardless of state
4. **Startup**: Manage startup items (limited on Windows Server)
5. **Tools**: Various diagnostic tools

### Advanced System Settings
Access via "View advanced system settings" search:
- **Performance Options**: Configure page file settings
- **Startup and Recovery**: Configure crash dump settings

**Questions:**
- What is the name of the service that lists Systems Internals as the manufacturer?
  - **Answer:** PsShutdown
- Whom is the Windows license registered to?
  - **Answer:** Windows User
- What is the command for Windows Troubleshooting?
  - **Answer:** `C:\Windows\System32\control.exe /name Microsoft.Troubleshooting`
- What command will open the Control Panel? (The answer is the name of .exe, not the full path)
  - **Answer:** `control.exe`

## Task 3: Change UAC Settings

User Account Control (UAC) settings can be adjusted through the System Configuration panel with four security levels:
1. Always notify (highest security)
2. Notify for apps (default)
3. Notify without dimming
4. Never notify (not recommended)

**Question:** What is the command to open User Account Control Settings? (The answer is the name of the .exe file, not the full path)
- **Answer:** `UserAccountControlSettings.exe`

## Task 4: Computer Management

Computer Management (compmgmt) utility contains three primary sections:

### System Tools
- **Task Scheduler**: Create and manage automated tasks
- **Event Viewer**: View system events and audit trails
- **Shared Folders**: View shared resources and connections
- **Local Users and Groups**: Manage user accounts (same as lusrmgr.msc)
- **Performance Monitor**: View performance data for troubleshooting
- **Device Manager**: Configure hardware devices

### Storage
- **Disk Management**: Perform advanced storage tasks (create, extend, shrink partitions)
- **Windows Server Backup**: Backup utilities

### Services and Applications
- **Services**: View and manage background services with different startup types (Automatic, Manual, Disabled)
- **WMI Control**: Configure Windows Management Instrumentation service

**Questions:**
- What is the command to open Computer Management? (The answer is the name of the .msc file, not the full path)
  - **Answer:** `compmgmt.msc`
- When is the npcapwatchdog scheduled task set to run at?
  - **Answer:** At system startup
- What is the name of the hidden folder that is shared?
  - **Answer:** `sh4r3dF0Ld3r`

## Task 5: System Information

Microsoft System Information (msinfo32) tool gathers comprehensive information about hardware, system components, and software environment.

### Key Sections
- **System Summary**: Hardware Resources, Components, Software Environment
- **Environment Variables**: System variables like WINDIR, ComSpec, etc.

**Questions:**
- What is the command to open System Information? (The answer is the name of the .exe file, not the full path)
  - **Answer:** `msinfo32.exe`
- What is listed under System Name?
  - **Answer:** `THM-WINFUN2`
- Under Environment Variables, what is the value for ComSpec?
  - **Answer:** `%SystemRoot%\system32\cmd.exe`

## Task 6: Resource Monitor

Resource Monitor (resmon) displays real-time information about:
- CPU usage
- Memory usage
- Disk usage
- Network usage
- File handles and modules
- Process analysis for deadlocks and file locking conflicts

**Question:** What is the command to open Resource Monitor? (The answer is the name of the .exe file, not the full path)
- **Answer:** `resmon.exe`

## Task 7: Command Prompt

Command Prompt (cmd) provides text-based interface for system interaction:

### Useful Commands
- **hostname**: Display computer name
- **whoami**: Display logged-in user
- **ipconfig**: Show network configuration
- **ipconfig /all**: Show detailed network information
- **netstat**: Display protocol statistics and network connections
- **net**: Manage network resources (use `net help` for sub-commands)

### Help Commands
- **/?**: Show help for commands (e.g., `ipconfig /?`)
- **cls**: Clear screen
- **net help**: Show help for net command

**Questions:**
- In System Configuration, what is the full command for Internet Protocol Configuration?
  - **Answer:** `C:\Windows\System32\cmd.exe /k %windir%\system32\ipconfig.exe`
- For the ipconfig command, how do you show detailed information?
  - **Answer:** `ipconfig /all`

## Task 8: Registry Editor

The Windows Registry is a hierarchical database storing configuration information for:
- User profiles
- Installed applications
- Hardware configuration
- Port usage

### Registry Editor
- Tool: `regedit` (or `regedt32.exe`)
- Warning: Advanced tool that can affect system operations if modified incorrectly

**Question:** What is the command to open the Registry Editor? (The answer is the name of the .exe file, not the full path)
- **Answer:** `regedt32.exe`
