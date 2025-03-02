# IIS Logs

## 1. Introduction
IIS (Internet Information Services) logs are critical for monitoring and investigating web server activity on Windows-based systems. These logs help in identifying security incidents, tracking user activities, and troubleshooting server issues.

## 2. Location of IIS Logs
By default, IIS logs are stored in:
```
C:\inetpub\logs\LogFiles\
```
Each website hosted on IIS has a unique folder inside this directory containing its respective logs.

## 3. IIS Log Format
IIS logs follow the W3C format and typically include:
```
date time c-ip cs-method cs-uri-stem sc-status cs(User-Agent)
```
Example log entry:
```
2024-03-02 12:00:45 192.168.1.10 GET /index.html 200 Mozilla/5.0
```
- **date/time**: Timestamp of the request.
- **c-ip**: Client IP address.
- **cs-method**: HTTP method used (GET, POST, etc.).
- **cs-uri-stem**: Requested resource.
- **sc-status**: HTTP response status code.
- **cs(User-Agent)**: Browser or client making the request.

## 4. Analyzing IIS Logs
### Identify Suspicious IPs
```powershell
Select-String -Path "C:\inetpub\logs\LogFiles\*.log" -Pattern "malicious_ip"
```

### Detect SQL Injection Attempts
```powershell
Select-String -Path "C:\inetpub\logs\LogFiles\*.log" -Pattern "SELECT|INSERT|DROP"
```

### Check for Brute-Force Login Attempts
```powershell
Select-String -Path "C:\inetpub\logs\LogFiles\*.log" -Pattern "POST /login"
```

## 5. Open-Source Tools for IIS Log Analysis
| Tool | Purpose |
|------|---------|
| **Microsoft Log Parser** | Parses and queries IIS logs |
| **GoAccess** | Real-time log analysis |
| **ELK Stack (Elasticsearch, Logstash, Kibana)** | Advanced log monitoring and visualization |
| **Log Parser Studio** | GUI-based log analysis tool from Microsoft |

## 6. Practical Steps for Investigating IIS Logs
1. **Collect Logs**: Retrieve log files from `C:\inetpub\logs\LogFiles\`.
2. **Search for Anomalies**: Identify unusual traffic patterns, failed login attempts, and SQL injection attempts.
3. **Correlate Events**: Cross-reference logs with system and network logs to detect coordinated attacks.
4. **Visualize Data**: Use tools like Kibana to visualize trends in log data.
5. **Report Findings**: Document suspicious activities and recommend mitigation steps.

## 7. Conclusion
IIS logs play a vital role in detecting security threats and diagnosing web server issues. Regular log analysis helps improve security posture, detect attacks early, and enhance forensic investigations.
