# Windows File Analysis

## Introduction
Windows file analysis is a crucial part of forensic investigations, helping analysts extract and examine files, metadata, and hidden artifacts. By analyzing file systems, timestamps, and file structures, forensic experts can uncover deleted data, trace user activities, and detect malicious activities.

## 1. Understanding Windows File Systems
Windows primarily uses the following file systems:
- **NTFS (New Technology File System)** – Supports file compression, encryption, and journaling.
- **FAT32 (File Allocation Table 32)** – Used in older systems and removable storage.
- **exFAT (Extended FAT)** – Optimized for flash drives.
- **ReFS (Resilient File System)** – Designed for large storage volumes and data integrity.

### Key File System Components
- **MFT (Master File Table)** – Stores metadata for each file in NTFS.
- **$LogFile** – NTFS transaction log file for system recovery.
- **$Recycle.Bin** – Stores deleted files before permanent removal.
- **Pagefile.sys** – Virtual memory file that may contain valuable forensic data.
- **Hiberfil.sys** – Stores system state during hibernation.

## 2. File Metadata Analysis
Metadata provides details about file creation, modification, and access.

### Extracting Metadata Using `fsutil`
```cmd
fsutil file queryfileid C:\Users\User\Documents\file.txt
```

### Viewing Timestamps with `dir`
```cmd
dir /T:C "C:\Users\User\Documents\file.txt"
```

### Analyzing Metadata with PowerShell
```powershell
Get-Item "C:\Users\User\Documents\file.txt" | Format-List *
```

## 3. Recovering Deleted Files
Deleted files may still exist on disk until overwritten. 

### Using Windows File Recovery
```cmd
winfr C: D: /regular /n Users\User\Documents\file.txt
```

### Using FTK Imager for Recovery
1. Open FTK Imager.
2. Select **File > Add Evidence Item**.
3. Choose **Logical Drive** and scan for deleted files.

## 4. File Signature and Hex Analysis
File headers (magic numbers) help identify file types, even if extensions are changed.

### Common File Signatures
| File Type | Hex Signature |
|-----------|--------------|
| JPEG      | `FF D8 FF E0`|
| PNG       | `89 50 4E 47`|
| PDF       | `25 50 44 46`|
| EXE       | `4D 5A`      |

### Viewing File Signatures with Hex Editor
1. Open file in **HxD or WinHex**.
2. Analyze the first few bytes to determine the file type.

## 5. Alternate Data Streams (ADS) in NTFS
NTFS allows hidden data storage in ADS, often used for hiding malware or extra information.

### Listing ADS with `dir`
```cmd
dir /r C:\Users\User\Documents\file.txt
```

### Extracting ADS Data
```cmd
type C:\Users\User\Documents\file.txt:secret.txt
```

## 6. Tools for Windows File Analysis
- **Autopsy** – Open-source forensic suite for file analysis.
- **FTK Imager** – Captures and examines disk images.
- **Sleuth Kit & Autopsy** – Extracts and analyzes file metadata.
- **HxD/WinHex** – Hex editors for examining raw file data.
- **Bulk Extractor** – Extracts hidden data from files.

## Conclusion
Windows file analysis plays a critical role in forensic investigations. Understanding file systems, metadata, deleted files, and hidden data streams allows forensic analysts to extract evidence effectively. Using a combination of command-line tools and specialized forensic software enhances the accuracy of investigations.

---
✅ **Always follow ethical guidelines and legal considerations when analyzing Windows file systems.**
