# Windows File System

## 1. Introduction
The Windows file system is a hierarchical structure used to store, manage, and access data on Windows operating systems. It supports multiple file formats and access control mechanisms.

---

## 2. Common File Systems in Windows
| File System | Description |
|-------------|-------------|
| **FAT16**   | An older file system with limited capacity and file size restrictions. |
| **FAT32**   | Supports larger files and volumes compared to FAT16 but lacks advanced features. |
| **exFAT**   | Optimized for flash drives; supports large file sizes and is cross-platform compatible. |
| **NTFS**    | Default file system for modern Windows systems; offers security, large volume support, and journaling. |
| **ReFS**    | Designed for resilience to corruption, optimized for storage spaces. |

---

## 3. Directory Structure in Windows
- **Root Directory (C:\)**: The top-level directory, typically the primary drive.
- Common directories:
  | Directory       | Description |
  |-----------------|-------------|
  | `C:\Windows`    | Core operating system files. |
  | `C:\Program Files` | Default location for installed applications. |
  | `C:\Users`      | Contains user-specific files and settings. |
  | `C:\Temp`       | Temporary files. |
  | `C:\System32`   | Critical system files and executables. |
  | `C:\Documents and Settings` | Legacy directory for user profiles (Windows XP). |

---

## 4. Features of Windows File Systems
- **Security:** File permissions and encryption via NTFS.
- **Journaling:** NTFS maintains a transaction log to recover data after a failure.
- **Compression:** NTFS supports file and folder compression.
- **Disk Quotas:** Administrators can set storage limits per user.
- **Large Volume Support:** NTFS can handle large files and partitions.
- **Data Integrity:** ReFS offers error correction and resilience.

---

## 5. File Types and Attributes
### File Types
| Type          | Description |
|---------------|-------------|
| **Text Files** | Contain readable text data (e.g., `.txt`). |
| **Executable Files** | Binary files that run programs (e.g., `.exe`, `.bat`). |
| **System Files** | Critical files for OS functioning (e.g., `.dll`, `.sys`). |
| **Configuration Files** | Store settings for applications (e.g., `.ini`, `.xml`). |
| **Compressed Files** | Archive files (e.g., `.zip`, `.rar`). |
| **Multimedia Files** | Images, videos, and audio (e.g., `.jpg`, `.mp4`). |

### File Attributes
- **Read-only (`R`)**: File can be read but not modified.
- **Hidden (`H`)**: File is not visible by default.
- **System (`S`)**: Critical for system operations.
- **Archive (`A`)**: Indicates that a file is ready for archiving.

Commands to change attributes:
```cmd
attrib +H file.txt
attrib -R file.txt
```

---

## 6. File Permissions
- Permissions control access to files and directories.
- NTFS permissions:
  - **Full Control:** Complete access.
  - **Modify:** Change and delete files.
  - **Read & Execute:** Open and execute files.
  - **List Folder Contents:** View folder contents.
  - **Read:** View file contents.
  - **Write:** Modify file contents.

### Managing Permissions
- **Right-click > Properties > Security tab:** Manage file permissions.
- **Command-line Tool:** `icacls`
  ```cmd
  icacls file.txt /grant user:F
  ```

---

## 7. Disk Management
### Partitioning and Formatting
- **Disk Management Tool:** GUI-based partitioning tool.
- **Command-line Tool:** `diskpart`
  ```cmd
  diskpart
  list disk
  select disk 0
  create partition primary
  format fs=ntfs
  ```

### Checking Disk Usage
- **Command:** `chkdsk`
  ```cmd
  chkdsk C: /f
  ```
  - `/f`: Fixes errors on the disk.

---

## 8. Mounting and Drive Letters
- Windows assigns drive letters (`C:`, `D:`) to partitions.
- Network drives can be mapped using `net use`:
  ```cmd
  net use Z: \\server\share
  ```

---

## 9. Backup and Recovery
- **File History:** Backs up user files.
- **System Restore:** Restores system settings to a previous state.
- **Backup and Restore:** Full system image backup.

---

## 10. Advanced Features
- **BitLocker:** Full disk encryption.
- **Storage Spaces:** Combine multiple drives into a storage pool.
- **ReFS (Resilient File System):** Enhanced reliability for storage.
- **Shadow Copy:** Provides snapshots of files for recovery.

---

## 11. Common Commands
| Command | Description |
|---------|-------------|
| `dir`   | List files and directories. |
| `cd`    | Change directory. |
| `copy`  | Copy files. |
| `move`  | Move files. |
| `del`   | Delete files. |
| `md`    | Create a directory. |
| `rd`    | Remove a directory. |
| `format`| Format a disk. |
| `chkdsk`| Check and repair disk errors. |
| `attrib`| Change file attributes. |
| `icacls`| Manage file permissions. |

---

## 12. Conclusion
The Windows file system, particularly with NTFS, provides robust features such as security, large file support, journaling, and advanced storage capabilities. Understanding its structure and commands is crucial for efficient system administration and troubleshooting.
