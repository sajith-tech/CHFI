# Acquire and Investigate RAM and Windows Registry Contents

## Introduction
Acquiring and analyzing volatile memory (RAM) and Windows Registry contents is crucial for forensic investigations. RAM analysis helps retrieve running processes, open network connections, and encryption keys, while the Windows Registry contains valuable system and user activity data.

## Acquiring RAM
### Tools for RAM Acquisition
- **FTK Imager**
- **DumpIt**
- **Magnet RAM Capture**
- **WinPmem**

### Steps to Acquire RAM Using FTK Imager
1. Download and install **FTK Imager**.
2. Open **FTK Imager** and go to **File > Capture Memory**.
3. Select the destination to save the RAM dump (`.mem` file).
4. Enable **Include pagefile** to capture swap memory.
5. Click **Capture Memory** to start the process.

### Acquiring RAM Using DumpIt (Command-line Tool)
1. Download **DumpIt.exe** and place it on the target system.
2. Run **DumpIt.exe** as administrator.
3. The memory dump (`.raw` file) will be saved in the same directory.

### Analyzing RAM Dump
Using **Volatility Framework**:
```bash
volatility -f memory.dmp imageinfo  # Identify OS profile
volatility -f memory.dmp pslist     # List running processes
volatility -f memory.dmp netscan    # List open network connections
volatility -f memory.dmp hashdump   # Extract password hashes
```

## Acquiring Windows Registry
### Important Windows Registry Hives
| Hive | Location | Purpose |
|------|---------|---------|
| `SAM` | `C:\Windows\System32\config\SAM` | Stores user account data |
| `SYSTEM` | `C:\Windows\System32\config\SYSTEM` | Contains system-wide settings |
| `SOFTWARE` | `C:\Windows\System32\config\SOFTWARE` | Stores installed software details |
| `SECURITY` | `C:\Windows\System32\config\SECURITY` | Manages security policies |
| `NTUSER.DAT` | `C:\Users\<Username>\NTUSER.DAT` | Contains user-specific settings |

### Acquiring Windows Registry Using `Regedit`
1. Open **Registry Editor** (`regedit.exe`).
2. Navigate to the hive you want to extract.
3. Click **File > Export**, and save it as a `.reg` file.

### Extracting Registry Hives Using Command Line
```powershell
reg save HKLM\SAM C:\Forensics\SAM.hiv
reg save HKLM\SYSTEM C:\Forensics\SYSTEM.hiv
reg save HKLM\SOFTWARE C:\Forensics\SOFTWARE.hiv
```

### Analyzing Registry Using RegRipper
1. Download and extract **RegRipper**.
2. Run the following command:
```bash
rip.exe -r SYSTEM.hiv -f system
rip.exe -r SOFTWARE.hiv -f software
```
3. Review the extracted data for user activity, installed software, and system configurations.

## Conclusion
Acquiring and analyzing RAM and Windows Registry data provides deep forensic insights. RAM analysis reveals active threats and live system artifacts, while registry investigation uncovers historical user activities and configuration changes.

---
✅ **Always ensure legal authorization before acquiring and analyzing memory or registry data.**
