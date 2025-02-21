# Analyze LNK Files

## Introduction
LNK (Shortcut) files in Windows store metadata about linked files and folders. They are useful in forensic investigations to track user activity, even if the original files are deleted.

## Location of LNK Files
LNK files are commonly found in:
- **User’s Recent Files folder:**
  ```
  C:\Users\{USERNAME}\AppData\Roaming\Microsoft\Windows\Recent\
  ```
- **Pinned and frequently accessed items:**
  ```
  C:\Users\{USERNAME}\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\
  ```

## Why LNK Files Matter in Forensics
- Store file paths, timestamps, and execution history.
- Reveal external device usage and file movement.
- Track user activities even if the file has been deleted.

## Analyzing LNK Files
### Using PowerShell
Extracting LNK metadata with PowerShell:
```powershell
$lnk = New-Object -ComObject WScript.Shell
$link = $lnk.CreateShortcut("C:\Users\{USERNAME}\Desktop\example.lnk")
$link | Format-List *
```

### Using Third-Party Tools
- **LNK Parser** – Extracts detailed metadata from LNK files.
- **FTK Imager** – Displays LNK file properties in forensic investigations.
- **ShellBags Explorer** – Cross-references LNK data with ShellBags.

## Interpretation of LNK Data
- **Target Path** – The file or folder the shortcut points to.
- **Timestamps** – Created, modified, and accessed times.
- **Volume Serial Number** – Identifies external devices.
- **Machine Name** – The system where the LNK file was created.

## Conclusion
LNK files serve as an essential forensic artifact in tracking user file interactions, external device usage, and deleted files.

---
✅ **Always follow ethical guidelines and legal considerations when analyzing LNK files.**
