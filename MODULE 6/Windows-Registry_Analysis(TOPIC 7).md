# Windows Registry Analysis

## Introduction
The Windows Registry is a hierarchical database that stores low-level system configurations, user preferences, and application settings. Analyzing the registry is crucial for forensic investigations as it contains valuable artifacts related to user activity, malware persistence, and system modifications.

## 1. Importance of Windows Registry Analysis
- **Tracks User Activity** – Stores recent files, executed programs, and login history.
- **Detects Malware Persistence** – Identifies registry keys used for malware execution.
- **Examines Installed Applications** – Provides insights into software installations and updates.
- **Recovers Deleted Data** – Some registry entries can persist even after deletion.
- **Investigates USB and Network Activity** – Records details of connected USB devices and network configurations.

## 2. Windows Registry Structure
The Windows Registry consists of five main hives:
- `HKEY_CLASSES_ROOT (HKCR)`: File associations and object linking.
- `HKEY_CURRENT_USER (HKCU)`: Settings for the logged-in user.
- `HKEY_LOCAL_MACHINE (HKLM)`: System-wide configurations and software installations.
- `HKEY_USERS (HKU)`: Settings for all user accounts.
- `HKEY_CURRENT_CONFIG (HKCC)`: Hardware configuration details.

### Important Registry Keys for Forensics
- **User Login History**: `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI`
- **Recently Accessed Files**: `HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`
- **Installed Applications**: `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`
- **Auto-Start Programs**: `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`
- **Connected USB Devices**: `HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR`

## 3. Tools for Registry Analysis
- **Windows Built-in Tools:**
  - `regedit` – Graphical interface for viewing/editing the registry.
  - `reg query` – Command-line tool for querying registry values.
- **Third-Party Tools:**
  - **RegRipper** – Automates registry analysis for forensics.
  - **Registry Explorer** – Advanced tool for viewing and analyzing registry hives.
  - **FTK Imager** – Extracts registry files for offline analysis.

## 4. Extracting and Analyzing Registry Hives
### A. Extracting Registry Hives Manually
Using the command prompt to export registry hives:
```cmd
reg save HKLM\SAM C:\Registry\sam.hiv
reg save HKLM\SYSTEM C:\Registry\system.hiv
reg save HKLM\SOFTWARE C:\Registry\software.hiv
```
This saves registry hives for offline analysis.

### B. Using RegRipper for Automated Analysis
```cmd
rip.exe -r C:\Registry\system.hiv -f system
```
This extracts forensic artifacts from the SYSTEM hive.

### C. Searching for Malware Persistence
```cmd
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```
This command lists programs set to run at startup.

## 5. Recovering Deleted Registry Keys
Even if a key has been deleted, traces may still exist in unallocated registry space. Tools like **Registry Explorer** and **Regripper** can help recover such data.

## Conclusion
Windows Registry analysis is a powerful technique in forensic investigations. It helps in reconstructing user activity, detecting malware persistence, and identifying system modifications. Tools like RegRipper and Registry Explorer assist in efficiently analyzing registry artifacts.

---
✅ **Always create a backup before modifying registry entries to prevent system damage.**
