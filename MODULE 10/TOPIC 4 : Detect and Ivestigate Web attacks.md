# Detect and Investigate Various Attacks on Web Applications

## 1. Introduction
Web applications are often targeted by attackers who exploit vulnerabilities to steal data, disrupt services, or gain unauthorized access. Detecting and investigating these attacks is crucial for securing web applications.

## 2. Common Web Application Attacks and Detection Methods

### 2.1 SQL Injection (SQLi)
- **Description**: Attackers inject malicious SQL queries into input fields to manipulate the database.
- **Detection**:
  - Analyze Apache logs for suspicious queries:
    ```bash
    grep -E "SELECT|INSERT|DROP|--|UNION" /var/log/apache2/access.log
    ```
  - Use Web Application Firewalls (WAF) like ModSecurity to filter SQLi attempts.

### 2.2 Cross-Site Scripting (XSS)
- **Description**: Attackers inject malicious JavaScript into web pages to steal user information.
- **Detection**:
  - Check logs for `<script>` tags or encoded payloads:
    ```bash
    grep -E "<script>|%3Cscript%3E" /var/log/apache2/access.log
    ```
  - Monitor browser console errors and user complaints about unexpected pop-ups.

### 2.3 Cross-Site Request Forgery (CSRF)
- **Description**: Attackers trick users into executing unwanted actions by leveraging their authenticated session.
- **Detection**:
  - Monitor HTTP request patterns for suspicious referrers.
  - Ensure CSRF tokens are validated in POST requests.

### 2.4 Brute Force Attacks
- **Description**: Attackers repeatedly attempt to guess user credentials.
- **Detection**:
  - Check for multiple failed login attempts from a single IP:
    ```bash
    grep "POST /login" /var/log/apache2/access.log | awk '{print $1}' | sort | uniq -c | sort -nr
    ```
  - Implement rate limiting and CAPTCHA mechanisms.

### 2.5 Remote File Inclusion (RFI) & Local File Inclusion (LFI)
- **Description**: Attackers include external or local files to execute malicious code.
- **Detection**:
  - Look for requests with `../../`, `file://`, or `http://` patterns:
    ```bash
    grep -E "\.\./|file://|http://" /var/log/apache2/access.log
    ```
  - Disable `allow_url_include` in PHP configurations.

### 2.6 Directory Traversal Attacks
- **Description**: Attackers access restricted files by exploiting poorly secured paths.
- **Detection**:
  - Identify log entries with `../` sequences:
    ```bash
    grep "../" /var/log/apache2/access.log
    ```
  - Ensure proper input validation and file access restrictions.

## 3. Open-Source Tools for Attack Investigation
| Tool | Purpose |
|------|---------|
| **GoAccess** | Real-time Apache log analysis |
| **ModSecurity** | Web application firewall |
| **SQLmap** | Detect and exploit SQLi vulnerabilities |
| **Burp Suite Community Edition** | Manual web security testing |
| **OWASP ZAP** | Automated web vulnerability scanning |
| **Fail2Ban** | Automated IP banning for brute-force prevention |

## 4. Steps to Investigate a Web Application Attack
1. **Collect Logs**: Retrieve Apache, Nginx, or IIS logs.
2. **Analyze Requests**: Look for suspicious patterns using `grep`, `awk`, and log analysis tools.
3. **Check User Behavior**: Identify unusual access times, locations, and request payloads.
4. **Use Security Tools**: Run security scans with OWASP ZAP, SQLmap, or Nikto.
5. **Mitigate and Secure**: Implement security patches, WAF rules, and monitoring alerts.

## 5. Conclusion
Web application forensics helps detect, investigate, and prevent attacks by analyzing logs and monitoring suspicious activities. Regular security audits and real-time monitoring enhance web application security.
