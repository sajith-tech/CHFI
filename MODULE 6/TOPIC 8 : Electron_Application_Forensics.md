# Electron Application Forensics

## Introduction
Electron applications are cross-platform desktop applications built using web technologies such as HTML, CSS, and JavaScript. Many popular applications like Slack, Discord, and Microsoft Teams are built using Electron. Forensic analysis of Electron applications can help in extracting user activity, chat logs, cached files, and credentials.

## 1. Importance of Electron Application Forensics
- **User Activity Tracking** – Identifies opened files, messages, and interactions.
- **Chat and Communication Analysis** – Extracts logs from Electron-based messaging applications.
- **Credential and Token Extraction** – Finds stored authentication tokens and passwords.
- **File and Cache Recovery** – Recovers temporary files and cached data used by the application.

## 2. Understanding Electron App Data Storage
Electron applications store data primarily in the following locations:
- **Local Storage** (`IndexedDB`, `LocalStorage`, `SessionStorage`)
- **SQLite Databases** (`.sqlite` files)
- **Cache and Logs** (`AppData` or `Application Support` folders)
- **Cookies and Session Data**

### Common Storage Paths
#### Windows
```
C:\Users\<username>\AppData\Roaming\<application-name>\
C:\Users\<username>\AppData\Local\<application-name>\
```
#### Linux
```
/home/<username>/.config/<application-name>/
```
#### macOS
```
/Users/<username>/Library/Application Support/<application-name>/
```

## 3. Key Artifacts in Electron Applications
- **Local Storage Data**: Contains user preferences and saved states.
- **IndexedDB & SQLite**: Stores persistent application data, including messages.
- **Cache & Logs**: Contains temporary files, user sessions, and potential deleted data.
- **Cookies & Session Tokens**: Authentication tokens that may allow account access.

## 4. Extracting Data from Electron Applications
### A. Extracting SQLite Databases
Most Electron apps use SQLite databases for data storage. Extracting relevant databases:
```cmd
sqlite3 C:\Users\<username>\AppData\Roaming\<app-name>\data.sqlite .dump
```
This extracts and displays stored data from the SQLite database.

### B. Analyzing IndexedDB
Use Chrome Developer Tools or external tools to inspect IndexedDB.
1. Open Developer Tools (`Ctrl + Shift + I` in Electron apps).
2. Navigate to **Application** → **IndexedDB**.
3. Review stored data related to user activities.

### C. Extracting Authentication Tokens
Electron apps may store authentication tokens in local storage or cookies:
```cmd
cat C:\Users\<username>\AppData\Roaming\<app-name>\Local Storage\leveldb\*.ldb
```
Tokens found can be used to investigate unauthorized access.

### D. Analyzing Cache Files
Electron-based apps cache user activity and media files in `Cache` and `Code Cache` folders. Extract cached data for forensic analysis:
```cmd
strings C:\Users\<username>\AppData\Local\<app-name>\Cache\*
```

## 5. Tools for Electron Application Forensics
- **DB Browser for SQLite** – Analyzes SQLite database files.
- **Chrome Developer Tools** – Extracts IndexedDB and LocalStorage data.
- **FTK Imager** – Extracts and analyzes application storage files.
- **Volatility** – Examines memory dumps for running Electron applications.
- **Recaf** – Extracts cache and logs from Electron applications.

## Conclusion
Electron application forensics provides insights into user interactions, stored credentials, and cached data. By analyzing storage locations, databases, and logs, forensic investigators can uncover critical evidence for security and incident response.

---
✅ **Ensure ethical and legal considerations when analyzing Electron-based applications.**
