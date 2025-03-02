# Web Application Forensics

## 1. Introduction
Web application forensics is the process of investigating security incidents, attacks, or unauthorized activities on web applications. It helps identify how an attack happened, what data was compromised, and who was responsible.

## 2. Common Web Attacks
Understanding common web attacks is crucial in forensic investigations:
- **SQL Injection (SQLi):** Attackers manipulate database queries to extract sensitive data.
- **Cross-Site Scripting (XSS):** Malicious scripts are injected into web pages to steal user information.
- **Cross-Site Request Forgery (CSRF):** Attackers trick users into executing unwanted actions.
- **File Inclusion (LFI/RFI):** Unauthorized files are included to execute malicious code.
- **Brute Force Attacks:** Automated attempts to crack login credentials.

## 3. Web Logs for Investigation
Web application forensic analysis heavily relies on logs. Important logs include:
- **Web Server Logs (Apache, Nginx, IIS)**: Record HTTP requests, IP addresses, user agents, and timestamps.
- **Application Logs:** Track internal application errors and user interactions.
- **Database Logs:** Record database queries and modifications.
- **Firewall Logs:** Capture blocked requests and intrusion attempts.

### Analyzing Web Logs
Use command-line tools to filter logs:
```bash
grep "SELECT" access.log   # Detect SQL Injection attempts
grep "<script>" access.log  # Identify XSS attacks
grep "POST /login" access.log | sort | uniq -c  # Check brute-force attempts
```

## 4. Open-Source Tools for Web Forensics
| Tool | Purpose |
|------|---------|
| **Logwatch** | Summarizes web server logs |
| **GoAccess** | Provides real-time web log analysis |
| **Nikto** | Scans for web vulnerabilities |
| **Burp Suite (Community Edition)** | Captures and analyzes web traffic |
| **sqlmap** | Detects and exploits SQL Injection vulnerabilities |

## 5. Practical Steps for Investigation
1. **Collect Evidence**: Gather logs, database dumps, and system snapshots.
2. **Analyze Web Logs**: Look for unusual patterns (e.g., excessive login failures, SQL injection attempts).
3. **Examine Database Activity**: Identify unauthorized access or modifications.
4. **Check File System Changes**: Detect unexpected file uploads or modifications.
5. **Inspect Network Traffic**: Use Wireshark to analyze suspicious HTTP requests.
6. **Report Findings**: Document attack vectors, affected data, and mitigation steps.

## 6. Conclusion
Web application forensics is essential for identifying security breaches and mitigating risks. By analyzing logs, detecting attack patterns, and using forensic tools, investigators can uncover malicious activities and strengthen web application security.
