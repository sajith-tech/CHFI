# Microsoft Azure Forensics

## 1. Introduction to Azure Forensics
Microsoft Azure Forensics involves the **detection, collection, and analysis** of digital evidence in Azure cloud environments. It helps investigators **track security incidents**, detect unauthorized access, and respond to cyber threats.

## 2. Key Challenges in Azure Forensics
- **Lack of Physical Access** – Investigators rely on logs and snapshots.
- **Shared Responsibility Model** – Customers and Microsoft share security responsibilities.
- **Dynamic Environment** – Virtual machines, containers, and serverless functions constantly change.
- **Data Collection Limitations** – Some logs are retained for a limited time.

## 3. Azure Forensic Data Sources
### a. **Azure Activity Logs**
   - Tracks changes to Azure resources.
   - Useful for **detecting unauthorized access or modifications**.
   - Collect logs using:
     ```bash
     az monitor activity-log list --output table
     ```

### b. **Azure Security Center Alerts**
   - Provides **real-time threat detection**.
   - Use **Azure Sentinel** for incident response.
   - View security alerts:
     ```bash
     az security alert list --output table
     ```

### c. **Azure Log Analytics**
   - Stores logs from multiple sources.
   - Useful for **event correlation and timeline analysis**.
   - Query logs using Kusto Query Language (KQL):
     ```kql
     SecurityEvent
     | where TimeGenerated > ago(24h)
     | where EventID == 4625 // Failed login attempts
     ```

### d. **Azure Network Security Group (NSG) Logs**
   - Logs inbound and outbound network traffic.
   - Helps **detect malicious IP addresses or unusual activity**.
   - Enable NSG logs:
     ```bash
     az network nsg flow-log create --nsg-name MyNSG --resource-group MyResourceGroup --storage-account MyStorage
     ```

### e. **Azure Virtual Machine (VM) Disk Forensics**
   - Capture VM disk snapshots for analysis.
   - Use **Azure Disk Forensics** to extract evidence:
     ```bash
     az snapshot create --resource-group MyResourceGroup --source MyVMOSDisk --name VMDiskSnapshot
     ```

### f. **Azure Storage Account Logs**
   - Tracks file uploads, downloads, and modifications.
   - Detects **data exfiltration or insider threats**.
   - View logs in Azure Storage Explorer.

## 4. Investigating Common Attacks in Azure
### a. **Unauthorized Access & Privilege Escalation**
   - Investigate failed logins:
     ```kql
     SigninLogs
     | where ResultType == "50053"
     ```
   - Review Azure AD sign-in logs.

### b. **Data Exfiltration**
   - Detect suspicious file transfers from storage accounts.
   - Analyze **Azure Storage Analytics Logs**.

### c. **Malware & Ransomware Attacks**
   - Examine **Azure Defender** alerts for malware activity.
   - Investigate compromised VMs by analyzing memory dumps.

### d. **Brute Force Attacks**
   - Check repeated failed login attempts in Azure AD logs.
   - Use **Microsoft Sentinel** for automated alerting.

## 5. Collecting Evidence in Azure
- **Use Azure CLI or PowerShell** to export logs.
- **Take snapshots of virtual disks** for forensic analysis.
- **Enable auditing for Azure SQL databases** to track changes.

## 6. Best Practices for Azure Forensics
- **Enable logging & monitoring** (Azure Security Center, Azure Sentinel).
- **Regularly collect & store forensic data** in an external system.
- **Implement incident response plans** tailored for cloud environments.
- **Use automation tools** for real-time detection and response.

## 7. Conclusion
Azure Forensics is essential for **investigating cyber incidents** in cloud environments. By leveraging **logs, security alerts, and forensic tools**, investigators can effectively detect and respond to threats in Azure.

---
