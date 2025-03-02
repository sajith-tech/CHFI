# Practical Guide: Analyzing Suspicious PDF & Microsoft Office Documents

## 1. Setting Up a Secure Environment
To analyze potentially malicious documents safely, use an **isolated virtual machine**:
- Install **Kali Linux** or **REMnux** in **VirtualBox/VMware**.
- Disable network access to prevent accidental infections.
- Use **snapshots** to restore the system if needed.

## 2. Open-Source Tools for Document Analysis
| Tool | Purpose |
|------|---------|
| **pdfid.py** | Detect JavaScript, launch actions in PDFs |
| **pdf-parser.py** | Extract embedded objects and scripts from PDFs |
| **OLETools (oleid, olevba)** | Analyze and extract macros from Office documents |
| **Didier Stevens Tools** | Analyze malicious PDFs and Word documents |
| **VirusTotal** | Scan document for known malware signatures |
| **YARA** | Detect malicious patterns in document files |

---

## 3. Analyzing a Suspicious PDF File
### **Step 1: Check PDF Metadata for Malicious Indicators**
```bash
pdfid.py sample.pdf
```
- Look for **JavaScript, OpenAction, and Launch actions**.

### **Step 2: Extract Embedded Objects and Streams**
```bash
pdf-parser.py -a sample.pdf
```
- Identify encoded or embedded suspicious content.

### **Step 3: Extract and Decode JavaScript from the PDF**
```bash
pdf-parser.py -f sample.pdf
```
- Analyze for obfuscated JavaScript executing commands.

---

## 4. Analyzing a Suspicious Microsoft Office Document
### **Step 1: Check for Macros in the Document**
```bash
oleid sample.doc
```
- Identify **macro-enabled (.docm, .xlsm, .pptm)** files.

### **Step 2: Extract VBA Macros**
```bash
olevba sample.doc
```
- Decode and analyze embedded macros.

### **Step 3: Analyze Macro Content for Suspicious Behavior**
```bash
olevba -a sample.doc
```
- Look for **AutoOpen, Shell, or PowerShell execution commands**.

### **Step 4: Extract Embedded Objects**
```bash
oleobj sample.doc
```
- Identify **hidden OLE objects, embedded executables, or scripts**.

---

## 5. Practical Exercise for Students
1. Set up a **Kali Linux** VM for testing.
2. Download a **test malicious PDF and Word document** from **MalwareBazaar**.
3. Use **pdfid.py** and **pdf-parser.py** to analyze the PDF.
4. Use **oleid** and **olevba** to analyze the Word document macros.
5. Identify embedded scripts or suspicious indicators.
6. Submit file hashes to **VirusTotal** to verify if it's flagged as malware.

---

## 6. Conclusion
By using open-source tools, students can learn to analyze and detect malicious document-based malware efficiently. Encourage hands-on testing and practical exercises to improve investigative skills.
