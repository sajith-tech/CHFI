# Collecting Windows Domain Information

## Introduction
Windows domain information is essential for forensic investigations in enterprise environments. It helps in understanding network structure, user authentication, and group policies that may impact security incidents.

## 1. Importance of Collecting Domain Information
- **User Authentication Analysis** – Tracks logins and potential unauthorized access.
- **Group Policy Analysis** – Identifies security configurations and restrictions.
- **Network Topology** – Maps relationships between domain controllers, servers, and workstations.
- **Audit Trails** – Helps in tracking malicious activity within the domain.

## 2. Key Sources of Domain Information
- **Active Directory (AD)**
- **Group Policies (GPOs)**
- **Domain Controllers (DCs)**
- **User and Group Accounts**
- **Event Logs**
- **Network Shares and Permissions**

## 3. Tools for Collecting Domain Information
- **Windows Built-in Commands** (PowerShell, WMIC, Command Prompt)
- **Sysinternals Suite** (PsExec, ADExplorer, AccessChk)
- **Third-Party Tools** (BloodHound, SharpHound, Nmap, LDAP queries)

## 4. Collecting Domain Information

### A. Identifying the Domain Controller
- **Using PowerShell:**
  ```powershell
  nltest /dclist:domainname
  ```
- **Using Command Prompt:**
  ```cmd
  echo %LOGONSERVER%
  ```
- **Checking Domain Controller Information:**
  ```powershell
  Get-ADDomainController -Filter *
  ```

### B. Listing Domain Users and Groups
- **Using PowerShell to list users:**
  ```powershell
  Get-ADUser -Filter * | Select-Object Name,SamAccountName,Enabled
  ```
- **Listing domain groups:**
  ```powershell
  Get-ADGroup -Filter * | Select-Object Name
  ```
- **Using WMIC to check user accounts:**
  ```powershell
  wmic useraccount get name,sid
  ```

### C. Extracting Group Policy Information
- **Checking applied GPOs:**
  ```powershell
  gpresult /R
  ```
- **Listing all GPOs in the domain:**
  ```powershell
  Get-GPO -All
  ```

### D. Checking Active Directory Structure
- **Using PowerShell to enumerate AD structure:**
  ```powershell
  Get-ADOrganizationalUnit -Filter * | Select-Object Name, DistinguishedName
  ```
- **Using LDAP queries:**
  ```powershell
  dsquery user -name *
  ```

### E. Gathering Event Logs for Authentication and Access Attempts
- **Checking recent logins:**
  ```powershell
  Get-EventLog -LogName Security -InstanceId 4624 -Newest 20
  ```
- **Auditing failed login attempts:**
  ```powershell
  Get-EventLog -LogName Security -InstanceId 4625 -Newest 20
  ```

### F. Checking Shared Network Resources
- **Listing shared folders and network drives:**
  ```powershell
  net share
  ```
- **Checking network connections:**
  ```powershell
  netstat -an
  ```

## 5. Storing and Preserving Domain Evidence
- Save collected data in a secure, forensic-safe location.
- Maintain logs and audit trails for future investigations.
- Use digital signatures and hashing (SHA-256) to verify data integrity.

## Conclusion
Collecting Windows domain information is crucial in forensic investigations to understand network security, user behavior, and potential threats. By leveraging built-in Windows tools and forensic utilities, investigators can efficiently extract, analyze, and document essential domain data.

---
✅ **Ensure proper permissions and legal compliance while collecting domain information.**
