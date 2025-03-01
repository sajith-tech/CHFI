# Windows 11 Event Log Analysis

## Introduction
Windows Event Logs are crucial forensic artifacts that store system, security, and application activity. Windows 11 logs provide insights into user actions, security events, and potential incidents.

## Location of Event Logs
Event logs are stored in the following location:
```
C:\Windows\System32\winevt\Logs\
```
Key log files include:
- **Security Logs:** `Security.evtx` (Tracks logins, policy changes, etc.)
- **System Logs:** `System.evtx` (Records system activities and failures)
- **Application Logs:** `Application.evtx` (Logs application errors and status)
- **PowerShell Logs:** `Microsoft-Windows-PowerShell/Operational.evtx` (PowerShell activity tracking)

## Why Event Logs Matter in Forensics
- Record login attempts and authentication failures.
- Provide a timeline of system activity.
- Identify execution of suspicious programs.
- Detect unauthorized access or malware activity.

## Analyzing Event Logs
### Using Event Viewer
1. Open **Event Viewer** (`eventvwr.msc`).
2. Navigate to **Windows Logs** → `Application`, `Security`, `System`, etc.
3. Use **Filters** to refine search (e.g., `4624` for logins, `1102` for log clearing).

### Using PowerShell
Extract specific event log data:
```powershell
Get-WinEvent -LogName Security -MaxEvents 20 | Format-List *
```

Find failed login attempts:
```powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} | Format-List
```

### Using Third-Party Tools
- **Event Log Explorer** – Advanced GUI-based log analysis.
- **LogParser** – Microsoft tool for querying event logs.
- **KAPE** – Automates collection of key forensic artifacts.

## Key Event IDs for Investigation
| Event ID | Description |
|----------|-------------|
| 4624 | Successful login |
| 4625 | Failed login attempt |
| 4720 | User account creation |
| 4722 | User account enabled |
| 4726 | User account deleted |
| 1102 | Event log cleared |
| 4688 | Process creation |
| 5140 | Network share access |

## Conclusion
Windows 11 Event Logs are a powerful forensic resource, enabling investigators to trace system activity, detect anomalies, and reconstruct security incidents.

---
✅ **Always follow ethical guidelines and legal considerations when analyzing event logs.**
