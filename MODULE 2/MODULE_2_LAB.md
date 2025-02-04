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

  
 ![Screenshot 2025-02-03 114829](https://github.com/user-attachments/assets/45f6df87-ab30-4fbd-9175-274bdf470ba3)

   
2. **Create a VHD**:
   - Click `Action > Create VHD` from the top menu.
   - Choose a location to save the VHD file (e.g., `C:\ForensicLab\TestDisk.vhd`).
   - Specify a size (e.g., 1 GB).
   - Select **Fixed size** for better performance.
   - Click `OK` to create the VHD.


![Disk Management 2_3_2025 10_36_09 AM](https://github.com/user-attachments/assets/43acfd01-962f-490c-881e-4fc0a1e51994)


3. **Initialize the Disk**:
   - Locate the new disk in Disk Management (it will say *Not Initialized*).
   - Right-click the disk and select `Initialize Disk`.
   - Choose **MBR** as the partition style and click `OK`.

![Disk Management 2_3_2025 10_41_24 AM](https://github.com/user-attachments/assets/1933f0a1-4ee7-464f-b320-655c0d5f937e)

![Disk Management 2_3_2025 10_42_16 AM](https://github.com/user-attachments/assets/8b8b78b6-d885-4424-b9a2-cce1183d8ec0)


4. **Create a Partition**:
   - Right-click the unallocated space on the VHD and choose `New Simple Volume`.
   - Follow the wizard to format the disk with **NTFS** and assign a drive letter.


![Disk Management 2_3_2025 10_43_23 AM](https://github.com/user-attachments/assets/6c1499c8-c8ce-48b4-a5ed-6090c211bce3)


---

### Step 2: Add Data to the VHD
1. **Mount the VHD**:
   - The VHD will now appear as a new drive in File Explorer (e.g., `E:\`).

2. **Copy Files**:
   - Add various files (e.g., documents, images, videos) to the drive for testing.
   
![New Volume (D_) - File Explorer 2_3_2025 10_47_15 AM](https://github.com/user-attachments/assets/b56dbef4-e84f-41b7-9aa9-38ce212aac10)

3. **Delete Some Files**:
   - Delete a few files and empty the Recycle Bin to simulate data loss.

---

### Step 3: Create a Forensic Image of the VHD
1. **Download and Install FTK Imager**:
   - Download FTK Imager from the official website.
   - Install and launch the tool.

![New Volume (D_) - File Explorer 2_3_2025 11_02_49 AM](https://github.com/user-attachments/assets/32c0de75-c0c8-494b-b5a8-3c7e808c6164)


2. **Create an Image**:
   - Click `File > Create Disk Image`.
     ![FTK Imager 4 7 3 81 - Brave 2_3_2025 11_04_38 AM](https://github.com/user-attachments/assets/801dbb0d-29f8-48f2-a7de-125901eafe46)
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

![Drive_Image Verify Results 2_3_2025 11_17_37 AM](https://github.com/user-attachments/assets/e7ee4b48-90cd-4c1a-8442-5532d0b12d7d)


2. **Scan the VHD**:
   - Open Recuva and select the mounted VHD drive (e.g., `E:\`).
   - Choose **Deep Scan** for a thorough analysis.
   - Start the scan and wait for it to complete.

![Drive_Image Verify Results 2_3_2025 11_21_06 AM](https://github.com/user-attachments/assets/56065880-f078-4deb-bdd8-819a38178bee)

![Recuva Wizard 2_3_2025 11_21_16 AM](https://github.com/user-attachments/assets/342ff97c-ff16-4b32-b205-de126acd9d75)


3. **Recover Files**:
   - Review the list of recoverable files.
   - Select the files you want to restore and choose a recovery location.

![Recuva 2_3_2025 11_23_53 AM](https://github.com/user-attachments/assets/dcd4e748-2613-4dc9-82ef-5b1cde84106b)


![Recuva 2_3_2025 11_25_15 AM](https://github.com/user-attachments/assets/8856d345-629a-4ed6-ae61-0891a54067fd)


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
