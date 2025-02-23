# Collecting Non-Volatile Information in Linux

Non-volatile information refers to data that remains on a system even after it is powered off. This data is crucial for forensic investigations and system auditing.

## 1. System Information
To get general system information:
```bash
uname -a
hostnamectl
```

## 2. OS and Kernel Details
To check OS version and kernel details:
```bash
cat /etc/os-release  # OS information
uname -r  # Kernel version
```

## 3. Installed Packages
To list installed software:
```bash
dpkg -l  # Debian-based systems
rpm -qa  # RedHat-based systems
```

## 4. User Accounts and Groups
To list user accounts:
```bash
cat /etc/passwd
```
To list group information:
```bash
cat /etc/group
```

## 5. Filesystem and Partition Details
To check disk partitions:
```bash
lsblk
fdisk -l
```
To list mounted filesystems:
```bash
mount
```

## 6. Services and Daemons
To list active services:
```bash
systemctl list-units --type=service  # Systemd systems
service --status-all  # Older systems
```

## 7. Startup Programs
To check programs that start at boot:
```bash
systemctl list-unit-files --type=service | grep enabled
chkconfig --list  # Older systems
```

## 8. SSH and Network Configuration
To view SSH configuration:
```bash
cat /etc/ssh/sshd_config
```
To check network settings:
```bash
cat /etc/network/interfaces  # Debian-based systems
cat /etc/sysconfig/network-scripts/ifcfg-*  # RedHat-based systems
```

## 9. Firewall Rules
To view firewall settings:
```bash
iptables -L -v -n  # Legacy firewall
firewall-cmd --list-all  # Firewalld
ufw status verbose  # UFW
```

## 10. Log Files
To check system logs:
```bash
cat /var/log/syslog  # General system logs
cat /var/log/auth.log  # Authentication logs
```

## 11. Scheduled Tasks (Cron Jobs)
To view scheduled jobs:
```bash
crontab -l  # User cron jobs
ls -la /etc/cron*  # System cron jobs
```

## 12. System Configuration Files
To check system-wide configuration:
```bash
ls /etc/
```

## Conclusion
Collecting non-volatile data is essential for forensic analysis, auditing, and security monitoring. The above commands help gather system information that persists even after a reboot.

