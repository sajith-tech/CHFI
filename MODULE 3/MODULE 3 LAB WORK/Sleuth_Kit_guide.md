# Complete Guide to Using Sleuth Kit in Linux

The Sleuth Kit (TSK) is a powerful collection of command-line tools used for forensic analysis of disk images and file systems. Below is a comprehensive guide to get started with Sleuth Kit in Linux.

---

## **Installation**
To install Sleuth Kit on Debian-based systems like Kali Linux or Parrot OS, run:

```bash
sudo apt update
sudo apt install sleuthkit
```

Verify the installation:

```bash
tsk_version
```

---

## **Key Sleuth Kit Tools and Commands**

### 1. **Listing Partitions (`mmls`)**
   Use `mmls` to display partition information in a disk image:

   ```bash
   mmls linux-image.dd
   ```

   This will show the partition layout with start and end sectors.

### 2. **Viewing File System Details (`fsstat`)**
   Get detailed information about a specific file system:

   ```bash
   fsstat -o <partition_start_sector> linux-image.dd
   ```

   Replace `<partition_start_sector>` with the correct offset from `mmls`.

### 3. **Extracting Files (`icat`)**
   Recover files by inode number:

   ```bash
   icat -o <partition_start_sector> linux-image.dd <inode_number> > recovered_file
   ```

   Example:

   ```bash
   icat -o 2048 linux-image.dd 45 > document.txt
   ```

### 4. **Listing Directory Contents (`fls`)**
   List directory and file entries, including deleted ones:

   ```bash
   fls -o <partition_start_sector> linux-image.dd
   ```

   Example:

   ```bash
   fls -o 2048 linux-image.dd
   ```

### 5. **Recovering Deleted Files (`tsk_recover`)**
   Recover all files, including deleted ones, to a directory:

   ```bash
   mkdir recovered_files
   tsk_recover -o <partition_start_sector> linux-image.dd recovered_files
   ```

### 6. **Analyzing Metadata (`istat`)**
   View metadata of a file by inode number:

   ```bash
   istat -o <partition_start_sector> linux-image.dd <inode_number>
   ```

   Example:

   ```bash
   istat -o 2048 linux-image.dd 12
   ```

### 7. **File System Walk (`tsk_loaddb` & `tsk_gettimes`)**
   Load file system metadata into a database for analysis:

   ```bash
   tsk_loaddb linux-image.dd database.db
   ```

   Extract file timestamps:

   ```bash
   tsk_gettimes -d database.db
   ```

---

## **Practical Tips**
- Always work on a copy of the disk image to avoid accidental modification.
- Use `grep` and `awk` to filter results from tools like `fls` or `tsk_gettimes`.
- Combine Sleuth Kit tools with other utilities like `Autopsy` for a graphical user interface.

---

This guide provides a strong foundation for forensic investigations using Sleuth Kit in Linux. Let me know if you need practical examples or advanced usage scenarios.
