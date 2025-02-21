# Windows ShellBags Forensics

## Introduction
Windows ShellBags are forensic artifacts stored in the Windows Registry. They record user interactions with folders, including access history, view settings, and navigation details. ShellBags are valuable in forensic investigations to track user activity, even if files or folders have been deleted.

## Location of ShellBags in the Registry
ShellBags are stored in the Windows Registry under the following locations:

- **For user-specific folders:**  
  ```
  HKEY_USERS\{SID}\Software\Microsoft\Windows\Shell\BagMRU  
  HKEY_USERS\{SID}\Software\Microsoft\Windows\Shell\Bags  
  ```
- **For folders accessed via Windows Explorer:**  
  ```
  HKEY_USERS\{SID}\Software\Microsoft\Windows\ShellNoRoam  
  ```
  
## Why ShellBags Matter in Forensics
- Tracks user folder navigation.
- Reveals interaction with removable media.
- Stores information even after folder deletion.
- Provides timestamp data about user activity.

## Analyzing ShellBags
### Using `Regedit`
1. Open **Registry Editor** (`regedit.exe`).
2. Navigate to `HKEY_USERS\{SID}\Software\Microsoft\Windows\Shell\BagMRU`.
3. Explore subkeys to view folder interaction details.

### Using PowerShell
Extracting ShellBag data using PowerShell:
```powershell
Get-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\Shell\BagMRU" | Format-List *
```

### Using Third-Party Tools
- **ShellBags Explorer** – Specialized tool to parse and visualize ShellBag data.
- **Autopsy** – Digital forensic platform that includes ShellBag analysis.
- **Registry Explorer** – Advanced registry analysis tool.

## Interpretation of ShellBag Data
- **MRUListEx** – Stores the order in which folders were accessed.
- **NodeSlot** – Assigns an index to a folder.
- **LastWriteTime** – Timestamp of last folder interaction.
- **ItemPos** – Stores folder view settings.

## Conclusion
Windows ShellBags provide critical forensic evidence by maintaining folder access history. Investigators use ShellBags to track deleted folder interactions and reconstruct user activity on a system.

---
✅ **Always follow ethical guidelines and legal considerations when analyzing ShellBag data.**
