# Collecting Non-Volatile Information in Windows

## Introduction
Non-volatile information refers to data that persists even after the system is powered off. This type of data is crucial for forensic investigations as it provides long-term evidence of system activity, file changes, and user interactions.

## 1. Importance of Non-Volatile Information
- **Persistent Data** – Remains intact even after a reboot.
- **Historical Analysis** – Helps in tracing past activities.
- **Legal Evidence** – Can be used in investigations and legal cases.

## 2. Key Sources of Non-Volatile Data
- **Disk Drives (HDD/SSD)**
- **Windows Registry**
- **Event Logs**
- **File Metadata**
- **Installed Applications and Services**
- **System Configuration and User Accounts**

## 3. Tools for Collecting Non-Volatile Data
- **Windows Built-in Commands** (WMIC, PowerShell, Command Prompt)
- **Sysinternals Suite** (Autoruns, RegRipper, LogParser)
- **Third-Party Forensic Tools** (FTK Imager, Autopsy, EnCase)

## 4. Collecting Non-Volatile Data

### A. Disk Analysis and File System Metadata
Disk analysis reveals deleted files, hidden partitions, and system logs.
- **Using FTK Imager to create a disk image:**
  1. Open FTK Imager.
  2. Select the drive to image.
  3. Choose a forensic format (E01, DD).
  4. Generate and verify hashes.
  ![FTK Imager](https://example.com/ftk-imager.png)

- **Using PowerShell to list drives:**
  ```powershell
  Get-PhysicalDisk
  ```

### B. Windows Registry Analysis
Registry analysis helps in tracking user activities, installed software, and system configurations.
- **Using RegRipper:**
  ```powershell
  rip.exe -r C:\Windows\System32\config\SOFTWARE -f software
  ```
- **Manually opening the registry:**
  1. Press `Win + R`, type `regedit`, and press Enter.
  2. Navigate through `HKEY_LOCAL_MACHINE` and `HKEY_USERS` hives.

### C. Extracting Event Logs
Event logs store login attempts, application errors, and system changes.
- **Using PowerShell to extract logs:**
  ```powershell
  wevtutil qe Security /c:100 /rd:true /f:text > C:\forensics\security_logs.txt
  ```
- **Using Event Viewer (`eventvwr.msc`) for manual analysis.**

### D. Identifying Installed Applications and Services
- **Using WMIC to list installed software:**
  ```powershell
  wmic product get name,version
  ```
- **Using PowerShell to check services:**
  ```powershell
  Get-Service | Where-Object { $_.Status -eq 'Running' }
  ```

### E. Analyzing User Accounts and System Configuration
- **Listing user accounts:**
  ```powershell
  net user
  ```
- **Checking system information:**
  ```powershell
  systeminfo > C:\forensics\system_info.txt
  ```

## 5. Storing and Preserving Evidence
- Store collected data securely in an external forensic drive.
- Maintain proper documentation and chain of custody.
- Use hashing techniques (MD5, SHA-256) to verify data integrity.

## Conclusion
Collecting non-volatile data is crucial in digital forensics as it provides permanent records of system activity. By utilizing forensic tools and Windows utilities, investigators can efficiently gather, analyze, and preserve critical evidence.

---
✅ **Ensure proper legal procedures are followed to maintain evidence integrity.**
