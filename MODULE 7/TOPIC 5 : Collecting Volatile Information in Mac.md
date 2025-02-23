# Collecting Volatile Information in Mac

Collecting volatile information in macOS is crucial for forensic investigations, as this data can change or disappear when the system is powered off. This process involves gathering system details, running processes, network connections, and active user activities.

## 1. System Information
To collect basic system details:
```bash
system_profiler SPHardwareDataType
sw_vers  # macOS version
uname -a  # Kernel version
uptime  # System uptime
```

## 2. Running Processes
To list all running processes:
```bash
ps aux
```
To monitor real-time system activity:
```bash
top -o cpu
```
To check active user sessions:
```bash
who -a
```

## 3. Network Connections
To view active network connections:
```bash
netstat -an
```
To check open network ports:
```bash
sudo lsof -i
```
To capture live network traffic:
```bash
tcpdump -i en0 -c 100 -w network_capture.pcap
```

## 4. Memory and Swap Information
To check memory usage:
```bash
vm_stat
sysctl hw.memsize
```
To list swap file usage:
```bash
sysctl vm.swapusage
```
To acquire a memory dump:
```bash
sudo sysdiagnose -f /path/to/save
```

## 5. Logged-in Users and System Logs
To list logged-in users:
```bash
w
who
```
To check recent logins:
```bash
last -10
```
To extract system logs:
```bash
log show --last 1h > system_logs.log
```

## 6. USB and External Devices
To check connected USB devices:
```bash
system_profiler SPUSBDataType
```
To list mounted storage devices:
```bash
df -h
```

## 7. Browser Activity and DNS Cache
To extract Safari browsing history:
```bash
sqlite3 ~/Library/Safari/History.db "SELECT * FROM history_items;"
```
To check DNS cache:
```bash
sudo killall -INFO mDNSResponder
```

## 8. Scheduled Tasks and Persistence
To list cron jobs:
```bash
crontab -l
```
To check launch agents and daemons:
```bash
ls /Library/LaunchAgents/
ls /Library/LaunchDaemons/
```

## Conclusion
Collecting volatile information in macOS is essential for forensic analysis. Using built-in macOS commands, investigators can gather real-time system data before it is lost or altered.

