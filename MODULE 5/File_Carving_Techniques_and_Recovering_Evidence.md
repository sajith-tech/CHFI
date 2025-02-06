# File Carving Techniques and Recovering Evidence from Deleted Partitions

## **Introduction**
File carving is a data recovery technique used in digital forensics to extract files based on content rather than file system metadata. This is particularly useful when investigating deleted partitions or corrupted file systems where metadata may be missing or damaged.

---

## **Objectives**
- Understand file carving techniques and their application.
- Learn methods for recovering evidence from deleted partitions.
- Explore tools commonly used in forensic analysis.

---

## **1. Understanding File Carving**
File carving involves scanning raw disk data to find files based on their structure, headers, and footers.

### **How It Works:**
- Identifies file signatures (specific byte patterns) at the start and end of files.
- Extracts the file data between these markers.
- Does not depend on file system metadata.

### **Common Use Cases:**
- Recovery from corrupted file systems.
- Evidence extraction after intentional data deletion.

---

## **2. File Carving Techniques**

### **Header-Footer Based Carving:**
- Searches for predefined headers and footers.
- Suitable for file formats like images, videos, and documents.

### **Content-Based Carving:**
- Relies on data patterns and context.
- Useful when headers and footers are missing.

### **Fragment Recovery:**
- Reassembles fragmented files based on known structures.

### **Tool-Assisted Carving:**
- Automated tools analyze storage devices and perform carving efficiently.

---

## **3. Tools for File Carving**

### **Open Source Tools:**
- **PhotoRec:** Recovers files from hard disks, memory cards, and other media.
- **Foremost:** Command-line tool for carving based on file headers, footers, and patterns.
- **Scalpel:** Successor to Foremost, optimized for speed.

### **Commercial Tools:**
- **X-Ways Forensics:** Powerful forensic software with advanced carving capabilities.
- **EnCase:** Comprehensive forensic analysis tool.
- **FTK Imager:** Image and analyze disk content, with file carving support.

---

## **4. Recovering Evidence from Deleted Partitions**
Deleted partitions often retain valuable data, even when inaccessible via standard file browsing.

### **Step 1: Create a Forensic Image**
- Use tools like **FTK Imager** or **dd** to create a bit-for-bit copy.
- Ensure write blockers are used to maintain data integrity.

### **Step 2: Analyze Partition Tables**
- Tools like **TestDisk** help identify and recover lost partitions.

### **Step 3: Carve Files from Raw Data**
1. Load the forensic image in a carving tool.
2. Specify file types to search for.
3. Extract and analyze the carved files.

### **Step 4: Validate and Document Findings**
- Verify the integrity and completeness of recovered files.
- Maintain a detailed log of actions and discoveries.

---

## **5. Best Practices for File Carving and Partition Recovery**
- **Preserve Original Evidence:** Work only on forensic copies.
- **Use Multiple Tools:** Different tools may yield varying results.
- **Document Processes:** Maintain detailed notes for chain of custody.
- **Validate Data Integrity:** Confirm that recovered files are complete and unaltered.

---

## **Conclusion**
File carving and partition recovery are indispensable techniques in digital forensics. By leveraging the right tools and methods, investigators can recover crucial evidence even from severely damaged or deleted storage media.

