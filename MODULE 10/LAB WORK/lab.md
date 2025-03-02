# Practical Guide: Detect and Investigate Web Application Attacks

## 1. Setting Up a Test Environment
To analyze web attacks practically, use open-source tools:
- **DVWA (Damn Vulnerable Web Application)** - A deliberately vulnerable web app.
- **bWAPP (Buggy Web Application)** - Another test environment with various vulnerabilities.
- **OWASP Mutillidae** - A free web security training environment.

**Setup on Kali Linux:**
```bash
sudo apt update && sudo apt install apache2 php mariadb-server -y
sudo systemctl start apache2
sudo systemctl start mariadb
sudo mysql_secure_installation
```

Clone a vulnerable web app:
```bash
git clone https://github.com/digininja/DVWA.git /var/www/html/dvwa
sudo chmod -R 777 /var/www/html/dvwa
```

## 2. Identifying Web Attacks

### 2.1 SQL Injection (SQLi)
- Use **SQLMap** to test for SQL injection:
  ```bash
  sqlmap -u "http://target.com/login.php?id=1" --dbs
  ```
- Investigate logs for SQLi payloads:
  ```bash
  grep -E "SELECT|UNION|INSERT|DROP" /var/log/apache2/access.log
  ```

### 2.2 Cross-Site Scripting (XSS)
- Use Burp Suite or OWASP ZAP to inject:
  ```html
  <script>alert('XSS')</script>
  ```
- Check logs for `<script>` or encoded payloads:
  ```bash
  grep -E "<script>|%3Cscript%3E" /var/log/apache2/access.log
  ```

### 2.3 Brute Force Attacks
- Use **Hydra** to simulate a brute force attack:
  ```bash
  hydra -l admin -P rockyou.txt http://target.com/login.php
  ```
- Investigate logs for repeated failed login attempts:
  ```bash
  grep "POST /login" /var/log/apache2/access.log | awk '{print $1}' | sort | uniq -c | sort -nr
  ```

### 2.4 Directory Traversal & LFI/RFI
- Use **Gobuster** to find hidden directories:
  ```bash
  gobuster dir -u http://target.com/ -w /usr/share/wordlists/dirb/common.txt
  ```
- Analyze logs for `../` sequences:
  ```bash
  grep "../" /var/log/apache2/access.log
  ```

## 3. Investigating Web Attacks
- Use **GoAccess** for real-time log monitoring:
  ```bash
  goaccess /var/log/apache2/access.log --log-format=COMBINED
  ```
- Use **ModSecurity** as a Web Application Firewall (WAF):
  ```bash
  sudo apt install libapache2-mod-security2
  sudo systemctl restart apache2
  ```

## 4. Mitigation and Defense
- **Update web applications** to patch vulnerabilities.
- **Enable security headers**:
  ```apache
  Header set X-XSS-Protection "1; mode=block"
  Header set X-Frame-Options "DENY"
  ```
- **Implement rate limiting** to prevent brute-force attacks.

## 5. Conclusion
By setting up a vulnerable environment and using open-source tools, students can learn how web attacks occur and how to investigate them effectively. Encourage students to analyze logs, use security scanners, and implement countermeasures.
