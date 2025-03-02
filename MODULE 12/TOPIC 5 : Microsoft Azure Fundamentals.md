
# Microsoft Azure Fundamentals

## 1. Introduction to Microsoft Azure
Microsoft Azure is a cloud computing platform that provides **on-demand computing services** like virtual machines, databases, storage, and AI solutions. It enables businesses to **build, deploy, and manage applications** without investing in physical infrastructure.

## 2. Key Features of Azure
- **Scalability** – Easily increase or decrease resources as needed.
- **Security & Compliance** – Built-in security tools and compliance with industry standards.
- **Global Reach** – Data centers available in multiple regions worldwide.
- **Cost Efficiency** – Pay-as-you-go pricing model.
- **Hybrid Cloud Support** – Integrates with on-premises infrastructure.

## 3. Azure Core Services
### a. **Compute Services**
- **Azure Virtual Machines (VMs)** – Runs Windows/Linux OS in the cloud.
- **Azure Functions** – Serverless computing for running small code snippets.
- **Azure Kubernetes Service (AKS)** – Manages containerized applications.

### b. **Storage Services**
- **Azure Blob Storage** – Stores unstructured data like images and videos.
- **Azure Files** – Fully managed file-sharing service.
- **Azure Disk Storage** – SSD/HDD storage for VMs.

### c. **Networking Services**
- **Azure Virtual Network (VNet)** – Securely connects Azure resources.
- **Azure Load Balancer** – Distributes network traffic.
- **Azure Firewall** – Protects against malicious attacks.

### d. **Database Services**
- **Azure SQL Database** – Managed relational database service.
- **Cosmos DB** – NoSQL database for globally distributed apps.
- **Azure Database for MySQL/PostgreSQL** – Fully managed open-source databases.

### e. **Identity & Security**
- **Azure Active Directory (Azure AD)** – Manages user authentication.
- **Azure Security Center** – Monitors security threats.
- **Azure Sentinel** – Cloud-native SIEM (Security Information and Event Management) tool.

## 4. Azure Deployment Models
- **Public Cloud** – Services are hosted in Microsoft’s data centers.
- **Private Cloud** – Dedicated resources for a single organization.
- **Hybrid Cloud** – Combines both public and private cloud benefits.

## 5. Azure Pricing & Cost Management
- **Pay-as-you-go** – Pay only for the resources used.
- **Reserved Instances** – Commit to a specific VM usage for lower costs.
- **Azure Cost Management** – Helps monitor and optimize cloud spending.

## 6. Getting Started with Azure
1. **Create a Free Azure Account** – Visit [portal.azure.com](https://portal.azure.com).
2. **Use the Azure CLI for Management**:
   ```bash
   az login
   az account show
   ```
3. **Deploy a Virtual Machine**:
   ```bash
   az vm create --name MyVM --image UbuntuLTS --resource-group MyResourceGroup --admin-username azureuser --generate-ssh-keys
   ```
4. **Monitor Resources using Azure Monitor**:
   ```bash
   az monitor metrics list --resource /subscriptions/{subscription-id}/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyVM
   ```

## 7. Benefits of Using Microsoft Azure
- **Highly Secure** – Advanced threat protection and compliance.
- **Multi-Layered Redundancy** – Ensures data availability.
- **AI & Machine Learning Capabilities** – Easily integrate with AI services.
- **Seamless Integration** – Works with Microsoft 365 and on-premises solutions.

## 8. Conclusion
Azure provides a **flexible, secure, and scalable** cloud computing platform for businesses of all sizes. Understanding its core components helps in leveraging cloud services effectively.

