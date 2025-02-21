# Windows Forensic Methodology

## Introduction
Windows forensics is the process of collecting, analyzing, and preserving digital evidence from Windows systems. It helps in investigating cybercrimes, insider threats, and unauthorized activities.

## 1. Initial Response
- **Identify the incident** – Understand the nature of the investigation.
- **Secure the scene** – Prevent tampering by isolating the affected system.
- **Document everything** – Note timestamps, user activity, and system status.
- **Ensure proper legal compliance** – Follow chain-of-custody procedures.

## 2. Data Acquisition
- **Live data acquisition** (if the system is running):
  - Use tools like FTK Imager, Magnet RAM Capture.
  - Capture volatile data: RAM, network connections, running processes.
  
- **Dead data acquisition** (if the system is off):
  - Create a forensic disk image using tools like Autopsy, EnCase.
  - Verify image integrity using hashes (MD5, SHA-256).
  
  

## 3. File System Analysis
- **Identify partitions** using `diskpart` or forensic tools.
- **Examine NTFS attributes** (Master File Table - `$MFT`).
- **Recover deleted files** using tools like Recuva, TestDisk.
- **Check for hidden files or encrypted partitions.**



## 4. Windows Registry Analysis
- **Registry stores system and user activity logs.**
- **Important registry hives:**
  - `NTUSER.DAT` (User activity, recent files, typed URLs)
  - `SYSTEM` (System configurations, connected USB devices)
  - `SOFTWARE` (Installed programs, user accounts)
  - `SECURITY` (Login policies, authentication logs)
- Use tools like RegRipper for analysis.



## 5. Log File Examination
- **Windows Event Logs (`.evtx` files)**
  - Security logs (`Security.evtx`) – Login attempts, policy changes.
  - System logs (`System.evtx`) – Device errors, shutdown events.
  - Application logs (`Application.evtx`) – Program crashes, malware activity.
- **Analyze logs with Event Viewer (`eventvwr.msc`) or PowerShell.**



## 6. User Activity Analysis
- **Check browsing history** – Edge, Chrome, Firefox store browsing logs.
- **Review recent files** – `RecentDocs`, `Jump Lists`.
- **Check USB device history** – `SYSTEM\CurrentControlSet\Enum\USBSTOR`.
- **Analyze Prefetch files (`C:\Windows\Prefetch`)** – Shows executed programs.



## 7. Memory Analysis
- **RAM analysis can reveal:**
  - Running processes.
  - Open network connections.
  - Unencrypted passwords.
- **Use tools like Volatility and Rekall for analysis.**



## 8. Malware and Persistence Analysis
- **Identify auto-start locations:**
  - Startup folder (`C:\Users\<User>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`)
  - Registry Run keys (`HKCU\Software\Microsoft\Windows\CurrentVersion\Run`)
- **Check scheduled tasks (`schtasks`) and services (`services.msc`).**
- **Scan for malware using Defender, Sysinternals tools (Autoruns, Process Explorer).**



## 9. Network Forensics
- **Analyze network logs:**
  - Firewall logs (`C:\Windows\System32\LogFiles\Firewall\pfirewall.log`)
  - Wireshark for packet capture.
- **Check active network connections using `netstat`, `TCPView`.**
- **Identify unauthorized remote access (RDP, SSH).**



## 10. Reporting and Documentation
- **Summarize findings with timestamps and logs.**
- **Include screenshots and hash values for integrity.**
- **Document chain of custody for legal cases.**
- **Prepare an executive summary with key findings.**



## Conclusion
Windows forensic investigations require a structured approach to collect, analyze, and preserve evidence effectively. By following this methodology, investigators can uncover security incidents and take appropriate actions.

---
### Tools Used in Windows Forensics:
- FTK Imager
- Autopsy
- Volatility
- RegRipper
- Event Viewer
- Wireshark
- Sysinternals Suite

---
✅ **Always ensure proper legal procedures are followed to maintain evidence integrity.**
