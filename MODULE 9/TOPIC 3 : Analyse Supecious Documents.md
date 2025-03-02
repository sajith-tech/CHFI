# Analyzing Suspicious Documents in Malware Forensics

## What is Document Malware Analysis?
Malware can be embedded in common document formats like **PDFs, Word (.doc/.docx), Excel (.xls/.xlsx), and PowerPoint (.ppt/.pptx)**. Analyzing these documents helps identify hidden malicious scripts, macros, or exploits used to infect systems.

---

## Why Analyze Suspicious Documents?
- **Documents are commonly used in phishing attacks.**
- **Embedded scripts or macros can execute malicious code.**
- **Hidden exploits can target software vulnerabilities.**
- **Documents may contain malicious links or payloads.**

---

## Steps to Analyze Suspicious Documents
### 1. **File Type Verification**
   - Identify the document format and integrity.
   - Use tools like **file, ExifTool** to check metadata.

### 2. **Hash Calculation & VirusTotal Scan**
   - Compute **MD5, SHA256** hashes.
   - Scan using **VirusTotal** to check for known threats.

### 3. **Metadata & Hidden Data Extraction**
   - Extract embedded metadata using **ExifTool, FOCA**.
   - Check for hidden objects, comments, or properties.

### 4. **Macro & Script Analysis**
   - If the document contains macros, extract and analyze them.
   - Tools: **oletools (olevba), OfficeMalScanner**.

### 5. **Embedded Object Extraction**
   - Extract images, scripts, and executables inside the document.
   - Tools: **Oledump, PDFid, pdf-parser**.

### 6. **Static and Behavioral Analysis**
   - Identify suspicious keywords, URLs, or shellcode.
   - Use **strings, YARA rules** to scan for known patterns.
   - Open in a sandboxed environment to observe behavior.

### 7. **Detecting Exploits and Payloads**
   - Check for vulnerabilities being exploited.
   - Look for shellcode or encoded payloads inside the document.
   - Tools: **PDFStreamDumper, peepdf, Didier Stevens tools**.

---

## Tools for Analyzing Suspicious Documents
1. **oletools** – Extracts macros from Office documents.
2. **pdf-parser** – Analyzes the structure of PDFs.
3. **Oledump** – Extracts and analyzes embedded objects.
4. **FOCA** – Extracts metadata from documents.
5. **VirusTotal** – Scans the document against multiple antivirus engines.
6. **YARA** – Detects malware patterns.

---

## Best Practices for Handling Suspicious Documents
- **Never open unverified documents directly.**
- **Use a sandboxed or isolated environment.**
- **Disable macros unless necessary.**
- **Keep software updated to patch vulnerabilities.**
- **Analyze email headers and metadata for phishing indicators.**

---

## Conclusion
Malicious documents are a common attack vector in cybercrime. Analyzing these files helps identify hidden threats, preventing infections and data breaches. Using proper forensic techniques and tools ensures effective detection and response.
