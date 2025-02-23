# Collecting Non-Volatile Information in Mac

Collecting non-volatile information in macOS involves gathering data that remains intact even after a system reboot. This data is crucial for forensic investigations as it includes file system artifacts, logs, user activities, installed applications, and more.

## 1. System Information
To collect detailed system information:
```bash
system_profiler > system_info.txt
sw_vers  # macOS version
uname -a  # Kernel version
```
To list startup services:
```bash
ls /Library/StartupItems/
ls /Library/LaunchAgents/
ls /Library/LaunchDaemons/
```

## 2. User and Account Information
To list all user accounts:
```bash
dscl . list /Users
```
To get details of a specific user:
```bash
dscl . -read /Users/username
```
To list all groups:
```bash
dscacheutil -q group
```
To check last logins:
```bash
last
```

## 3. File System and Storage Information
To list file system details:
```bash
df -h
mount
```
To locate large or recently modified files:
```bash
find / -type f -size +100M  # Files larger than 100MB
find / -type f -mtime -7  # Files modified in the last 7 days
```
To list hidden files:
```bash
ls -la ~/Library/
```

## 4. Log Analysis
To retrieve system logs:
```bash
log show --info --debug > system_logs.txt
```
To view authentication logs:
```bash
cat /var/log/secure.log
```
To check application logs:
```bash
tail -f /var/log/system.log
```

## 5. Installed Applications and Packages
To list installed applications:
```bash
ls /Applications/
```
To list installed packages:
```bash
pkgutil --pkgs
```
To check recently installed packages:
```bash
ls -lt /var/db/receipts/
```

## 6. Network Configuration and Artifacts
To list network interfaces:
```bash
ifconfig -a
```
To check saved Wi-Fi networks:
```bash
networksetup -listpreferredwirelessnetworks en0
```
To list firewall settings:
```bash
sudo defaults read /Library/Preferences/com.apple.alf globalstate
```

## 7. External Devices and USB History
To check connected USB devices:
```bash
system_profiler SPUSBDataType
```
To list mounted storage devices:
```bash
diskutil list
```
To view previously connected devices:
```bash
ls /Volumes/
```

## 8. Browser and Internet History
To extract Safari browsing history:
```bash
sqlite3 ~/Library/Safari/History.db "SELECT * FROM history_items;"
```
To check saved credentials in Keychain:
```bash
security find-generic-password -ga 'example.com'
```

## 9. Scheduled Tasks and Cron Jobs
To list scheduled tasks:
```bash
crontab -l
launchctl list
```
To check persistent startup items:
```bash
ls /Library/LaunchAgents/
ls /Library/LaunchDaemons/
```

## Conclusion
Collecting non-volatile information in macOS is essential for forensic investigations. It helps in reconstructing system activities, tracking user actions, and identifying suspicious events that persist beyond system reboots.

