
# AWS Forensics

## 1. Introduction to AWS Forensics
AWS forensics is the process of investigating security incidents in Amazon Web Services (AWS). It involves collecting and analyzing logs, snapshots, and system data to identify unauthorized access, data breaches, or malicious activities.

## 2. Challenges in AWS Forensics
- **Lack of Physical Access**: Cloud infrastructure is managed by AWS.
- **Ephemeral Resources**: Instances and logs can be deleted quickly.
- **Shared Responsibility Model**: AWS secures the cloud, but customers must secure their own data and configurations.
- **Data Location Issues**: Data may be stored in multiple regions.

## 3. Key AWS Forensics Artifacts
### a. CloudTrail Logs (User Activity Logs)
- Records all API calls and user actions in AWS.
- Stored in S3 and can be analyzed using **Athena** or **CloudWatch**.
- **Example Query in AWS Athena:**
  ```sql
  SELECT eventTime, eventName, userIdentity.arn, sourceIPAddress 
  FROM cloudtrail_logs 
  WHERE eventTime > '2025-01-01T00:00:00Z';
  ```

### b. CloudWatch Logs (System and Application Logs)
- Stores logs from AWS services and applications.
- Can be used to detect unauthorized access attempts and system errors.
- **Example Command:**
  ```bash
  aws logs describe-log-groups
  aws logs get-log-events --log-group-name "/var/log/apache2/access.log"
  ```

### c. AWS GuardDuty (Threat Detection)
- Identifies suspicious activities like:
  - Unusual API calls.
  - Compromised IAM credentials.
  - Malicious traffic.

### d. S3 Access Logs
- Tracks read/write activities on AWS S3 buckets.
- Useful for detecting unauthorized access or data exfiltration.
- **Example Analysis Command:**
  ```bash
  grep "s3.amazonaws.com" s3_access_logs.txt
  ```

### e. EC2 Snapshots & Memory Forensics
- Create **snapshots** of EC2 instances for forensic investigation.
- Use tools like **Volatility** for RAM analysis.
- **Creating a Snapshot:**
  ```bash
  aws ec2 create-snapshot --volume-id vol-1234567890abcdef0
  ```

### f. VPC Flow Logs (Network Traffic Analysis)
- Captures inbound and outbound traffic in AWS.
- Helps detect **port scanning**, **DDoS attacks**, and **data exfiltration**.
- **Enable VPC Flow Logs:**
  ```bash
  aws ec2 create-flow-logs --resource-ids vpc-xxxxxx --resource-type VPC --traffic-type ALL --log-destination arn:aws:logs:region:account-id:log-group/vpc-flow-logs
  ```

## 4. AWS Forensics Investigation Process
### a. Incident Detection
- Enable **GuardDuty**, **CloudTrail**, and **VPC Flow Logs**.
- Monitor logs for unusual activity (e.g., failed login attempts, privilege escalation).

### b. Data Collection
- Collect **CloudTrail logs, EC2 snapshots, S3 logs, and IAM activity logs**.
- Dump memory of a running EC2 instance for forensic analysis.

### c. Data Analysis
- **Use Athena** to analyze large logs.
- **Use ELK Stack (Elasticsearch, Logstash, Kibana)** for visualization.
- **Use Volatility** for RAM forensics.

### d. Mitigation & Response
- Revoke compromised IAM credentials.
- Restrict network access using security groups.
- Patch vulnerabilities and apply best security practices.

## 5. AWS Security Best Practices
- **Enable MFA (Multi-Factor Authentication)** for all accounts.
- **Use IAM Roles** instead of access keys.
- **Encrypt Data** using AWS KMS (Key Management Service).
- **Enable Logging** for all AWS services.
- **Regularly Audit IAM Permissions**.

## 6. Conclusion
AWS forensics helps in detecting and responding to security incidents. By leveraging logs, snapshots, and monitoring tools, security teams can identify and mitigate threats effectively.

---
