
# Google Cloud Forensics

## 1. Introduction to Google Cloud Forensics
Google Cloud Forensics is the process of **detecting, collecting, analyzing, and preserving digital evidence** from Google Cloud Platform (GCP) environments. It is used for investigating security incidents, detecting unauthorized access, and responding to cyber threats.

## 2. Challenges in Google Cloud Forensics
- **Limited Log Retention** – Some logs are not stored indefinitely.
- **Ephemeral Resources** – Cloud instances and containers may not persist.
- **Data Collection Constraints** – Cloud-based evidence requires proper access permissions.
- **Shared Responsibility Model** – Security is shared between Google and the user.

## 3. Key Forensic Data Sources in GCP
### a. **Google Cloud Audit Logs**
   - Tracks activity across GCP services.
   - Useful for **detecting unauthorized access or changes**.
   - Query logs using:
     ```bash
     gcloud logging read "logName:cloudaudit.googleapis.com%2Factivity" --format json
     ```

### b. **Google Cloud Identity and Access Management (IAM) Logs**
   - Records user authentication and access attempts.
   - Detects **privilege escalation or unauthorized API calls**.
   - View IAM policies:
     ```bash
     gcloud projects get-iam-policy my-project
     ```

### c. **Google Cloud Storage Logs**
   - Tracks file uploads, downloads, and modifications.
   - Helps **detect data exfiltration or insider threats**.
   - Enable logging:
     ```bash
     gcloud storage buckets update my-bucket --log-bucket my-log-bucket
     ```

### d. **Google Cloud Compute Engine (GCE) Disk Snapshots**
   - Capturing VM disk snapshots for forensic analysis.
   - Helps in **malware and ransomware investigations**.
   - Create a snapshot:
     ```bash
     gcloud compute disks snapshot my-disk --snapshot-names forensic-snapshot
     ```

### e. **Google VPC Flow Logs**
   - Monitors network traffic in GCP.
   - Helps detect **malicious IPs, data exfiltration, or C2 communication**.
   - Enable flow logs:
     ```bash
     gcloud compute networks subnets update my-subnet --enable-flow-logs
     ```

### f. **Google Cloud Security Command Center (SCC)**
   - Provides security alerts for **threat detection**.
   - Helps in **incident response and attack investigation**.

## 4. Investigating Common Attacks in GCP
### a. **Unauthorized Access & Privilege Escalation**
   - Analyze IAM activity logs for **suspicious privilege modifications**.
   - Detect failed authentication attempts:
     ```bash
     gcloud logging read 'protoPayload.methodName="google.iam.v1.SetIamPolicy"' --format json
     ```

### b. **Data Exfiltration**
   - Check **Cloud Storage logs** for unusual data transfers.
   - Investigate network logs for high outbound traffic.

### c. **Brute Force & Password Spraying Attacks**
   - Analyze IAM logs for repeated failed login attempts.
   - Use Google Security Command Center alerts.

### d. **Malware & Ransomware Attacks**
   - Capture and analyze **VM snapshots** for signs of malware.
   - Investigate security alerts from **Google Cloud Security Scanner**.

## 5. Collecting Evidence in Google Cloud
- **Export logs to BigQuery** for deep analysis:
  ```bash
  gcloud logging sinks create my-sink bigquery.googleapis.com/projects/my-project/datasets/my-dataset
  ```
- **Capture snapshots of Compute Engine disks** for forensic analysis.
- **Use Google Takeout** to extract user account data for investigations.

## 6. Best Practices for Google Cloud Forensics
- **Enable and retain logs** in Cloud Logging.
- **Use Google Cloud Security Command Center** for real-time threat detection.
- **Regularly monitor IAM permissions** to prevent privilege abuse.
- **Automate threat detection** using **Chronicle Security Operations**.

## 7. Conclusion
Google Cloud Forensics is essential for **incident response and security investigations** in cloud environments. By leveraging **logs, security tools, and forensic techniques**, investigators can effectively detect, analyze, and respond to cyber threats in GCP.
