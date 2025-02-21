# Memory Forensics in Windows

## Introduction
Memory forensics is the process of analyzing volatile memory (RAM) to uncover forensic artifacts such as running processes, network connections, and malicious activities. It is a crucial part of digital investigations, especially in detecting advanced malware, rootkits, and fileless attacks.

## 1. Importance of Memory Forensics
- **Uncover Malware and Rootkits** – Detect hidden processes and malicious code.
- **Analyze Running Processes** – Identify suspicious programs in real-time.
- **Recover Encryption Keys and Passwords** – Extract sensitive data stored in RAM.
- **Investigate Network Connections** – Track active connections and communication.
- **Detect Fileless Attacks** – Identify threats that do not leave artifacts on disk.

## 2. Tools for Memory Forensics
- **Windows Built-in Tools:**
  - `tasklist` – Lists running processes.
  - `wmic process list` – Detailed process information.
  - `netstat -ano` – View active network connections.
- **Third-Party Tools:**
  - **Volatility** – Open-source memory analysis framework.
  - **Rekall** – Advanced memory forensic framework.
  - **DumpIt** – Lightweight memory acquisition tool.
  - **Magnet RAM Capture** – Collects RAM for forensic analysis.

## 3. Acquiring Memory Dump
To analyze memory, a forensic investigator first needs to capture a memory dump from a live Windows system. 

### A. Using DumpIt
1. Download DumpIt and run it as an administrator.
2. The tool will automatically create a memory dump file (e.g., `memory.dmp`).

### B. Using WinPMEM
```cmd
winpmem.exe -o memory.raw
```
This command captures the full RAM dump and saves it as `memory.raw`.

### C. Using PowerShell to Check Running Processes
```powershell
Get-Process | Format-Table -AutoSize
```
This command lists all active processes.

## 4. Analyzing Memory Dumps with Volatility
Volatility is a powerful tool used for in-depth memory analysis.

### A. Checking System Profile
```cmd
volatility -f memory.raw imageinfo
```
This helps determine the correct profile for analysis.

### B. Listing Running Processes
```cmd
volatility -f memory.raw --profile=Win10x64 pslist
```
This command retrieves the list of running processes.

### C. Checking Network Connections
```cmd
volatility -f memory.raw --profile=Win10x64 netscan
```
This command extracts active network connections from memory.

### D. Dumping Process Executables
```cmd
volatility -f memory.raw --profile=Win10x64 procdump -p 1234 -D output_folder
```
This extracts the executable of a suspicious process (replace `1234` with the process ID).

### E. Extracting Cached Passwords
```cmd
volatility -f memory.raw --profile=Win10x64 hashdump
```
Retrieves stored password hashes from memory.

## 5. Detecting Malware and Suspicious Activity
- **Compare process lists using `pslist` and `psscan` to find hidden processes.**
- **Use `malfind` to detect injected code:**
  ```cmd
  volatility -f memory.raw --profile=Win10x64 malfind
  ```
- **Use `dlllist` to examine DLLs loaded into processes:**
  ```cmd
  volatility -f memory.raw --profile=Win10x64 dlllist -p 1234
  ```

## Conclusion
Memory forensics in Windows plays a vital role in uncovering advanced threats, malware infections, and forensic artifacts. Using tools like Volatility and DumpIt, investigators can extract and analyze RAM dumps to gather crucial evidence in digital investigations.

---
✅ **Always acquire memory dumps before shutting down a system to prevent data loss.**
