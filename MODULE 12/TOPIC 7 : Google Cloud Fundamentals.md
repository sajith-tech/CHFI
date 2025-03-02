
# Google Cloud Fundamentals

## 1. What is Google Cloud?
Google Cloud Platform (GCP) is a suite of **cloud computing services** provided by Google that runs on the same infrastructure that Google uses internally for its end-user products like Google Search, YouTube, and Gmail. It offers **compute, storage, networking, security, and AI/ML** services.

## 2. Key Features of Google Cloud
- **Scalability** – Easily scale resources up or down.
- **Security** – Built-in security and compliance standards.
- **Global Infrastructure** – Data centers across multiple regions.
- **Pay-as-You-Go Pricing** – Only pay for what you use.
- **AI & Machine Learning** – Advanced AI services for automation.

## 3. Core Services in Google Cloud
Google Cloud provides various services across different domains:

### a. **Compute Services**
- **Compute Engine** – Virtual machines (VMs) for running applications.
- **Google Kubernetes Engine (GKE)** – Managed Kubernetes for containerized applications.
- **Cloud Functions** – Serverless computing for event-driven applications.

### b. **Storage Services**
- **Cloud Storage** – Object storage for unstructured data.
- **Persistent Disks** – Block storage for Compute Engine VMs.
- **Filestore** – Managed file storage for enterprise applications.

### c. **Networking Services**
- **Virtual Private Cloud (VPC)** – Private network for resources.
- **Cloud Load Balancing** – Distributes traffic across servers.
- **Cloud CDN** – Improves web application performance.

### d. **Database Services**
- **Cloud SQL** – Managed relational databases like MySQL, PostgreSQL.
- **Firestore** – NoSQL document database for real-time applications.
- **BigQuery** – Serverless data warehouse for analytics.

### e. **Security & Identity**
- **IAM (Identity & Access Management)** – Manage user permissions.
- **Cloud Security Command Center** – Threat detection & monitoring.
- **DLP (Data Loss Prevention)** – Protect sensitive information.

### f. **AI & Machine Learning**
- **Vertex AI** – Build, deploy, and scale ML models.
- **Cloud AutoML** – Train ML models without extensive coding.
- **AI APIs** – Pre-trained models for vision, speech, and language.

## 4. Google Cloud Global Infrastructure
Google Cloud operates in multiple **regions** and **zones** to ensure **low latency and high availability**.
- **Region** – A specific geographical area (e.g., `us-central1`).
- **Zone** – A data center within a region (e.g., `us-central1-a`).

## 5. Google Cloud Pricing Model
Google Cloud follows a **pay-as-you-go** model:
- **Sustained Use Discounts** – Discounts for continuous usage.
- **Committed Use Contracts** – Prepaid discounts for reserved resources.
- **Free Tier** – Limited free usage of Google Cloud services.

## 6. Getting Started with Google Cloud
### a. **Sign Up for a Free Google Cloud Account**
   - Visit [Google Cloud Console](https://console.cloud.google.com/)
   - Get **$300 free credits** for 90 days.
   - Enable **billing** to access more services.

### b. **Using Google Cloud SDK**
Install the Google Cloud SDK on your machine:
```bash
curl https://sdk.cloud.google.com | bash
exec -l $SHELL
gcloud init
```
Check available services:
```bash
gcloud services list
```

## 7. Why Use Google Cloud?
- **Performance** – Fast networking and compute power.
- **Security** – Enterprise-grade security & compliance.
- **Integration** – Works with **hybrid and multi-cloud** environments.
- **Innovation** – Access to **AI, ML, and data analytics tools**.

## 8. Conclusion
Google Cloud is a powerful cloud platform with **scalable, secure, and cost-effective solutions** for businesses and developers. Understanding its fundamentals helps in **deploying applications, managing infrastructure, and leveraging AI capabilities**.
