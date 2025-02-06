# Practical Session: Analyze File System of Linux and Windows Evidence Image, Recover Deleted Files, and Analyze File Formats

## Objective:
The goal of this session is to help students understand how to analyze a forensic image of Linux and Windows file systems, recover deleted files, and analyze various file formats to identify hidden data or artifacts.

---

## Overview:
1. **Analyze Linux File System (ext4) Evidence Image**
2. **Analyze Windows File System (NTFS) Evidence Image**
3. **Recover Deleted Files**
4. **Analyze Common File Formats (PDF, Word, etc.)**

---

## Prerequisites:
- A virtual machine or physical system running Kali Linux or any forensic tool (e.g., Autopsy, FTK Imager).
- Evidence images for Linux (ext4) and Windows (NTFS) file systems.
- Basic knowledge of file systems (ext4, NTFS).
- Tools: Sleuth Kit, Autopsy, FTK Imager, Hex Editors, etc.

---

## Section 1: Analyze Linux File System (ext4) Evidence Image

### Step 1: Set Up Your Environment
1. Boot up Kali Linux or your forensic machine.
2. Install necessary tools if not already installed:
   ```bash
   sudo apt-get update
   sudo apt-get install sleuthkit autopsy

### Step 2: Mount the Evidence Image
1. Create a mount point for the image:
   ```bash
   mkdir /mnt/forensic
   ```
2. Mount the image to analyze the file system:
   ```bash
   sudo mount -o loop /path/to/linux-image.dd /mnt/forensic
   ```
   Replace `/path/to/linux-image.dd` with the path to your evidence image.

### Step 3: Analyze File System Structure
1. List the files and directories in the mounted image:
   ```bash
   ls /mnt/forensic
   ```
2. Use **Sleuth Kit** to perform detailed analysis of the file system:
   - Use `fls` to list the files in the image:
     ```bash
     fls -r /path/to/linux-image.dd
     ```
   - Use `istat` to view inode details of a specific file:
     ```bash
     istat /path/to/linux-image.dd <inode_number>
     ```

### Step 4: Recover Deleted Files
1. Use **The Sleuth Kit’s** `icat` to recover deleted files:
   - First, identify the block where the file resides:
     ```bash
     fsstat /path/to/linux-image.dd
     ```
   - Recover the file using `icat`:
     ```bash
     icat /path/to/linux-image.dd <inode_number> > recovered_file
     ```

### Step 5: Analyze File System Metadata
1. Look at metadata using **fls** to get timestamps (creation, modification, last access times) for files:
   ```bash
   fls -m /mnt/forensic
   ```

---

## Section 2: Analyze Windows File System (NTFS) Evidence Image

### Step 1: Mount the Evidence Image
1. Mount the Windows NTFS image using a similar process:
   ```bash
   mkdir /mnt/windows
   sudo mount -o loop /path/to/windows-image.dd /mnt/windows
   ```

### Step 2: Analyze File System Structure
1. Use **Autopsy** or **Sleuth Kit** to analyze the file system:
   - Use `fls` for listing files in an NTFS image:
     ```bash
     fls -r /path/to/windows-image.dd
     ```

2. **View the MFT (Master File Table)** for detailed file information:
   ```bash
   mmls /path/to/windows-image.dd
   ```

### Step 3: Recover Deleted Files
1. **Recover files** using Sleuth Kit’s `icat` (for NTFS):
   - Identify the file location using `fls` and `istat`.
   - Use `icat` to recover files:
     ```bash
     icat /path/to/windows-image.dd <inode_number> > recovered_file
     ```

### Step 4: Analyze File System Metadata
1. Use Autopsy to examine the file metadata like timestamps, file sizes, and owner details.
2. Retrieve deleted file evidence using **Sleuth Kit’s** `tsk_recover` tool.

---

## Section 3: Recover Deleted Files from Linux and Windows Systems

### Step 1: Understanding Deleted Files
- **Linux**: When a file is deleted, its inode is marked as free, but the data blocks may not be overwritten immediately.
- **Windows**: When a file is deleted, its entry is removed from the MFT, but the data might still exist on the disk until it’s overwritten.

### Step 2: Recovering Deleted Files from Linux
1. Use **Sleuth Kit’s `fls`** to list deleted files:
   ```bash
   fls -d /path/to/linux-image.dd
   ```
2. Recover the deleted file using `icat`:
   ```bash
   icat /path/to/linux-image.dd <inode_number> > recovered_file
   ```

### Step 3: Recovering Deleted Files from Windows
1. Use **Autopsy** to search for deleted files.
2. **Analyze the MFT** for deleted records.
3. **Sleuth Kit’s `icat`** can be used to recover data from unallocated space or free clusters.

---

## Section 4: Analyze File Formats

### Step 1: Use a Hex Editor to Analyze Files
1. Open the file with a hex editor (e.g., `Hex Fiend`, `GHex`).
2. Inspect the **magic numbers** (file signatures) at the start of the file. For example:
   - PDF files begin with `25 50 44 46` (hexadecimal representation of `%PDF`).
   - JPEG images begin with `FF D8 FF`.

### Step 2: PDF Analysis
1. Examine the structure of a PDF file, looking for metadata, embedded objects, or hidden information.
2. Extract embedded files using tools like **pdf-parser**.

### Step 3: Word File Analysis
1. For `.docx` files (XML format), unzip the file and analyze its components (e.g., `word/document.xml`, `docProps/core.xml`).
2. Look for hidden text or metadata using a hex editor.

### Step 4: PowerPoint and Excel File Analysis
1. For `.pptx` and `.xlsx` files (XML format), unzip the file and analyze the embedded XML components (e.g., `xl/worksheets/sheet1.xml`).
2. Check for hidden slides, cells, or embedded macros.

---

## Tools Used:
- **Autopsy**: A GUI tool for analyzing evidence images and file system structures.
- **Sleuth Kit**: A collection of command-line tools for forensic analysis of disk images.
- **Hex Editors**: Used for inspecting and analyzing file headers (e.g., GHex, Hex Fiend).
- **FTK Imager**: A forensic imaging tool for creating and analyzing disk images.
- **Foremost**: A tool for recovering deleted files from a disk image.

---

## Conclusion:
- By the end of this session, students should have hands-on experience in mounting, analyzing, and recovering deleted files from Linux and Windows evidence images.
- They should also be able to inspect and analyze common file formats (PDF, Word, Excel, etc.) to identify any hidden or malicious data.

---

## Additional Notes:
- **Always maintain a forensic chain of custody** while working with evidence images.
- Encourage students to use write blockers to avoid modifying original evidence during analysis.
- Students should be familiar with tools like **Autopsy** and **Sleuth Kit**, as they are commonly used in forensic investigations.
```


