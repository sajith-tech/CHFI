# Mac Forensics

Mac forensics involves the analysis of macOS systems to collect digital evidence, investigate security incidents, and detect malicious activities. It includes examining file systems, logs, memory, and network activity.

## 1. Collecting System Information
To gather basic system details:
```bash
system_profiler SPHardwareDataType
sw_vers  # macOS version
uname -a  # Kernel version
```

## 2. User and Account Information
To list users and groups:
```bash
dscl . list /Users  # List all users
dscacheutil -q group  # List all groups
```

## 3. Process and Memory Analysis
To check running processes:
```bash
ps aux
```
To monitor real-time system activity:
```bash
top
```
To acquire a memory dump:
```bash
sudo sysdiagnose -f /path/to/save
```

## 4. File System and Metadata Analysis
To list files with detailed metadata:
```bash
ls -lO /Users
mdls /path/to/file  # Get file metadata
```
To analyze file changes:
```bash
fs_usage -w > filesystem_activity.log
```

## 5. Log Analysis
To view system logs:
```bash
log show --info --debug | grep "error"
```
To check authentication logs:
```bash
cat /var/log/secure.log
```
To view application logs:
```bash
tail -f /var/log/system.log
```

## 6. Browser and Internet History
To extract Safari browsing history:
```bash
sqlite3 ~/Library/Safari/History.db "SELECT * FROM history_items;"
```
To check DNS cache:
```bash
sudo killall -INFO mDNSResponder
```

## 7. USB and External Device Analysis
To list USB devices:
```bash
system_profiler SPUSBDataType
```
To check mounted devices:
```bash
mount
```

## 8. Network Analysis
To view open network connections:
```bash
netstat -an
```
To check active network services:
```bash
lsof -i
```
To capture network traffic:
```bash
tcpdump -i en0 -w capture.pcap
```

## 9. Persistence Mechanisms
To check startup items:
```bash
ls /Library/StartupItems/
ls /Library/LaunchAgents/
ls /Library/LaunchDaemons/
```
To list cron jobs:
```bash
crontab -l
```

## 10. Disk and File Recovery
To list deleted files:
```bash
sudo find / -name "*.deleted"
```
To recover deleted files:
```bash
sudo photorec
```

## Conclusion
Mac forensics is essential for digital investigations involving macOS systems. By using built-in commands and forensic tools, investigators can collect critical evidence, analyze system behavior, and detect anomalies.

