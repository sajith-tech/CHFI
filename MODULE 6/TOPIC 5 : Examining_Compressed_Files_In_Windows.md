# Examining Compressed Files in Windows

## Introduction
Compressed files are commonly used to reduce file size and bundle multiple files together. In forensic investigations, examining compressed files helps uncover hidden or deleted data, analyze metadata, and detect potential malware.

## 1. Importance of Examining Compressed Files
- **Data Recovery** – Extract deleted or hidden files.
- **Malware Analysis** – Identify malicious payloads hidden inside archives.
- **Metadata Extraction** – Retrieve timestamps and file details.
- **Password Protection Bypass** – Investigate encrypted or protected archives.

## 2. Common Compressed File Formats
- **ZIP (.zip)** – Commonly used for general compression.
- **RAR (.rar)** – Supports advanced compression and encryption.
- **7z (.7z)** – High compression ratio with AES encryption.
- **TAR (.tar, .gz, .bz2)** – Common in Linux and macOS systems.
- **CAB (.cab)** – Used in Windows installations.

## 3. Tools for Examining Compressed Files
- **Windows Built-in Tools**
  - `tar.exe` (Windows 10+)
  - `expand.exe` (For CAB files)
  - `PowerShell` cmdlets
- **Third-Party Tools**
  - WinRAR, 7-Zip, PeaZip (GUI-based tools)
  - `binwalk` (For forensic analysis of embedded files)
  - `foremost` and `bulk_extractor` (For data carving)

## 4. Examining Compressed Files

### A. Listing Contents of a Compressed File
- **Using PowerShell for ZIP Files:**
  ```powershell
  Expand-Archive -LiteralPath "C:\example.zip" -DestinationPath "C:\output" -WhatIf
  ```
- **Using Command Prompt:**
  ```cmd
  tar -tf archive.tar
  ```
- **Using 7-Zip to list files:**
  ```cmd
  7z l archive.zip
  ```

### B. Extracting Compressed Files
- **Extract ZIP using PowerShell:**
  ```powershell
  Expand-Archive -LiteralPath "C:\example.zip" -DestinationPath "C:\output"
  ```
- **Extract RAR using WinRAR Command Line:**
  ```cmd
  unrar x archive.rar C:\output
  ```
- **Extract TAR files in Windows:**
  ```cmd
  tar -xvf archive.tar -C C:\output
  ```

### C. Searching for Keywords Inside Compressed Files
- **Using PowerShell to search within extracted files:**
  ```powershell
  Select-String -Path "C:\output\*.*" -Pattern "sensitive_keyword"
  ```
- **Using `binwalk` for deep analysis:**
  ```cmd
  binwalk -e archive.zip
  ```

### D. Analyzing Metadata and Hidden Files
- **Using `exiftool` to check metadata:**
  ```cmd
  exiftool archive.zip
  ```
- **Finding hidden files in ZIP archives:**
  ```cmd
  7z h archive.zip
  ```

### E. Extracting Password-Protected Archives
- **Brute-force ZIP passwords using John the Ripper:**
  ```cmd
  zip2john archive.zip > hash.txt
  john --wordlist=rockyou.txt hash.txt
  ```
- **Using `rarcrack` for RAR files:**
  ```cmd
  rarcrack archive.rar --type rar
  ```

## 5. Storing and Preserving Evidence
- Ensure extracted data integrity by calculating hashes.
- Store original and extracted files separately.
- Document findings, timestamps, and file details.

## Conclusion
Examining compressed files in Windows forensic investigations is crucial for recovering hidden data, analyzing malware, and extracting metadata. By using built-in Windows tools and third-party forensic utilities, investigators can efficiently analyze compressed files and uncover valuable evidence.

---
✅ **Always preserve the original compressed file and work on copies to maintain forensic integrity.**
