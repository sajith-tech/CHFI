# Linux Hash Value Generation and Calculation Tools

## Command-Line Tools

### **1. md5sum**
- Generate MD5 hashes for files or input.
- **Usage:**
  ```bash
  md5sum filename.txt
  ```

### **2. sha256sum, sha1sum, sha512sum**
- Generate SHA hashes (SHA-1, SHA-256, SHA-512).
- **Usage:**
  ```bash
  sha256sum filename.txt
  ```
  Replace `sha256sum` with `sha1sum` or `sha512sum` for other variations.

### **3. openssl**
- Multi-purpose cryptographic tool.
- **Usage for SHA-256:**
  ```bash
  openssl dgst -sha256 filename.txt
  ```
- **Usage for MD5:**
  ```bash
  openssl dgst -md5 filename.txt
  ```

### **4. cksum**
- Computes a CRC checksum of a file.
- **Usage:**
  ```bash
  cksum filename.txt
  ```

### **5. b2sum**
- Computes BLAKE2 hash values.
- **Usage:**
  ```bash
  b2sum filename.txt
  ```

### **6. hashdeep**
- Recursively generate and audit MD5, SHA-1, and SHA-256 hashes.
- **Usage:**
  ```bash
  hashdeep -c sha256 -r directory/
  ```

### **7. xxd (Hex Dump Tool)**
- Can indirectly help calculate and manipulate file hex data for hash analysis.
- **Usage:**
  ```bash
  xxd filename.txt | sha256sum
  ```

### **8. certutil (via mono-utils)**
- Used for generating cryptographic hashes, often available by installing mono packages.
- **Usage:**
  ```bash
  certutil -hashfile filename.txt SHA256
  ```

## Graphical Tools

### **1. GtkHash**
- Lightweight GUI application for calculating file checksums.
- Supports MD5, SHA family, and other algorithms.

### **2. HashCalc (cross-platform via Wine)**
- Calculate MD5, CRC32, SHA values with an easy GUI.

## Additional Notes
- Always verify hash values to ensure file integrity and authenticity.
- Consider combining these tools with shell scripts for automation in forensic or security tasks.



