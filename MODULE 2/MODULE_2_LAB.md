# Lab: Create a Hard Disk File for Forensics and Recover Data

## Objective

Simulate a forensic scenario by creating a hard disk file, adding data, and recovering deleted data using open-source tools on a Windows system.

---

## Prerequisites

1. A Windows PC with administrative privileges.
2. Internet connection to download tools.
3. Open-source tools:
   - **FTK Imager**: For creating and analyzing disk images.
   - **Recuva**: For recovering deleted files.
   - **Disk Management** (built-in Windows tool): For creating virtual disks.

---

## Steps

### Step 1: Create a Virtual Hard Disk (VHD)
1. **Open Disk Management**:
   - Press `Win + R`, type `diskmgmt.msc`, and press Enter.
   
2. **Create a VHD**:
   - Click `Action > Create VHD` from the top menu.
   - Choose a location to save the VHD file (e.g., `C:\ForensicLab\TestDisk.vhd`).
   - Specify a size (e.g., 1 GB).
   - Select **Fixed size** for better performance.
   - Click `OK` to create the VHD.

3. **Initialize the Disk**:
   - Locate the new disk in Disk Management (it will say *Not Initialized*).
   - Right-click the disk and select `Initialize Disk`.
   - Choose **MBR** as the partition style and click `OK`.

4. **Create a Partition**:
   - Right-click the unallocated space on the VHD and choose `New Simple Volume`.
   - Follow the wizard to format the disk with **NTFS** and assign a drive letter.

---

### Step 2: Add Data to the VHD
1. **Mount the VHD**:
   - The VHD will now appear as a new drive in File Explorer (e.g., `E:\`).

2. **Copy Files**:
   - Add various files (e.g., documents, images, videos) to the drive for testing.

3. **Delete Some Files**:
   - Delete a few files and empty the Recycle Bin to simulate data loss.

---

### Step 3: Create a Forensic Image of the VHD
1. **Download and Install FTK Imager**:
   - Download FTK Imager from the official website.
   - Install and launch the tool.

2. **Create an Image**:
   - Click `File > Create Disk Image`.
   - Select `Logical Drive` and click `Next`.
   - Choose the VHD drive (e.g., `E:\`) and click `Finish`.
   - Select a destination to save the image file (e.g., `C:\ForensicLab\VHD_Image.E01`).

3. **Verify the Image**:
   - FTK Imager will calculate hash values (e.g., MD5, SHA-1) to verify the image integrity.

---

### Step 4: Recover Deleted Files
1. **Download and Install Recuva**:
   - Download Recuva from the official website.
   - Install and launch the tool.

2. **Scan the VHD**:
   - Open Recuva and select the mounted VHD drive (e.g., `E:\`).
   - Choose **Deep Scan** for a thorough analysis.
   - Start the scan and wait for it to complete.

3. **Recover Files**:
   - Review the list of recoverable files.
   - Select the files you want to restore and choose a recovery location.

---

## Additional Notes

- **Preserving Evidence**:
  - Always work on copies of evidence files to maintain integrity.
- **Hash Verification**:
  - Use FTK Imager to verify hash values before and after recovery.
- **Documentation**:
  - Maintain detailed notes of every step for reporting purposes.

---

## Conclusion

This lab demonstrates how to create a virtual hard disk, simulate data deletion, and recover lost files using open-source tools. It provides hands-on experience in handling digital evidence, a critical skill in computer forensics.
