
# Forensic Acquisition of Amazon EC2, Azure VM, and GCP VM

## Introduction
Forensic acquisition of cloud-based virtual machines (VMs) is crucial for **incident response, security investigations, and evidence preservation**. This guide covers **open-source methods** to acquire forensic images from Amazon EC2 (AWS), Azure VM, and Google Cloud VM (GCP).

---

# 1. Forensic Acquisition of AWS EC2 Instance

### **1.1. Snapshot-Based Acquisition**
Amazon EC2 instances store data on **Elastic Block Store (EBS) volumes**. A forensic copy can be created by taking an **EBS snapshot**.

#### **Step 1: Identify the Volume Attached to the Instance**
```bash
aws ec2 describe-instances --instance-ids i-xxxxxxxxxxxxxxxx
```
- Note the **Volume ID** associated with the instance.

#### **Step 2: Create a Snapshot of the Volume**
```bash
aws ec2 create-snapshot --volume-id vol-xxxxxxxxxxxx --description "Forensic snapshot"
```
- This creates a read-only snapshot of the volume.

#### **Step 3: Create a New Volume from Snapshot**
```bash
aws ec2 create-volume --snapshot-id snap-xxxxxxxxxxxx --availability-zone us-east-1a
```
- Attach this volume to a **forensic analysis VM**.

#### **Step 4: Mount and Acquire Image**
```bash
mkdir /mnt/forensic_volume
sudo mount /dev/xvdf1 /mnt/forensic_volume
sudo dd if=/dev/xvdf1 of=aws_ec2_image.dd bs=4M status=progress
```
- The `dd` command creates a **forensic disk image**.

---

# 2. Forensic Acquisition of Microsoft Azure VM

Azure virtual machines use **Managed Disks**. A forensic acquisition can be done by creating a **disk snapshot**.

### **2.1. Snapshot-Based Acquisition**
#### **Step 1: Identify the Disk Associated with the VM**
```bash
az vm show --name VM_NAME --resource-group RESOURCE_GROUP --query "storageProfile.osDisk.managedDisk.id"
```
- Note the **Disk ID**.

#### **Step 2: Create a Snapshot of the Disk**
```bash
az snapshot create --resource-group RESOURCE_GROUP --name forensic_snapshot --source DISK_ID --location eastus
```

#### **Step 3: Create a New Disk from Snapshot**
```bash
az disk create --resource-group RESOURCE_GROUP --name forensic_disk --source forensic_snapshot --location eastus
```
- Attach this disk to a **forensic VM**.

#### **Step 4: Mount and Acquire Image**
```bash
sudo mkdir /mnt/azure_disk
sudo mount /dev/sdc1 /mnt/azure_disk
sudo dd if=/dev/sdc1 of=azure_vm_image.dd bs=4M status=progress
```
- The forensic image is now ready for analysis.

---

# 3. Forensic Acquisition of Google Cloud VM (GCP)

Google Cloud VMs use **Persistent Disks**. A forensic copy can be created by **taking a snapshot** and attaching it to a forensic VM.

### **3.1. Snapshot-Based Acquisition**
#### **Step 1: Identify the Disk Associated with the Instance**
```bash
gcloud compute instances describe INSTANCE_NAME --zone us-central1-a --format="get(disks.deviceName)"
```

#### **Step 2: Create a Snapshot of the Disk**
```bash
gcloud compute disks snapshot DISK_NAME --snapshot-names forensic-snapshot
```

#### **Step 3: Create a New Disk from the Snapshot**
```bash
gcloud compute disks create forensic-disk --source-snapshot forensic-snapshot --zone us-central1-a
```
- Attach this disk to a **forensic VM**.

#### **Step 4: Mount and Acquire Image**
```bash
sudo mkdir /mnt/gcp_disk
sudo mount /dev/sdb1 /mnt/gcp_disk
sudo dd if=/dev/sdb1 of=gcp_vm_image.dd bs=4M status=progress
```
- The forensic image is now stored for investigation.

---

# 4. Integrity Verification and Analysis
Once acquisition is complete, verify the integrity of the forensic image:

```bash
sha256sum aws_ec2_image.dd
sha256sum azure_vm_image.dd
sha256sum gcp_vm_image.dd
```

For forensic analysis, use tools like:
- **Autopsy** – GUI-based forensic analysis tool.
- **Volatility** – Memory forensics.
- **Plaso (log2timeline)** – Log analysis.
- **FTK Imager** – Disk image analysis.

---

# 5. Conclusion
By using **open-source tools**, forensic investigators can acquire and analyze cloud VM instances from AWS, Azure, and GCP in a legally sound and efficient manner. Cloud forensics plays a critical role in **cybercrime investigations and incident response**.
