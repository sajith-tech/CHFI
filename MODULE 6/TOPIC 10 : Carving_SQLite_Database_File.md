# Carving SQLite Database Files

## Introduction
SQLite databases are widely used in web browsers, mobile applications, and various software to store structured data. Forensic analysts often need to carve SQLite database files to recover deleted records and extract valuable forensic artifacts.

## 1. Importance of SQLite Database Forensics
- **Recovering Deleted Data** – Extracts deleted records that may not be visible in standard queries.
- **Identifying User Activity** – Finds browsing history, messages, credentials, and more.
- **Investigating Corrupted Files** – Recovers and repairs damaged SQLite files.
- **Extracting Embedded Data** – Extracts files, logs, and metadata stored in SQLite databases.

## 2. Common SQLite Database Locations
SQLite databases are used in multiple applications, including web browsers, messaging apps, and system logs.

### Web Browsers (Google Chrome, Firefox, Edge)
- **History**: `History`, `places.sqlite`
- **Cookies**: `Cookies`, `cookies.sqlite`
- **Logins**: `Login Data`, `logins.json`
- **Form Autofill**: `Web Data`, `formhistory.sqlite`

### Messaging Apps (WhatsApp, Telegram, Skype)
- **Chat History**: `msgstore.db`, `main.db`
- **User Accounts**: `accounts.db`
- **Call Logs**: `calls.db`

### System Files
- **Windows Registry and Logs**: `AppCompatCache.db`, `eventlog.db`
- **MacOS User Data**: `/Users/<username>/Library/Application Support/`
- **Android App Data**: `/data/data/<app-name>/databases/`

## 3. Carving Deleted Records from SQLite Databases
When data is deleted in SQLite, it remains in the database file until it is overwritten. Carving tools help retrieve these records.

### A. Using SQLite Commands to Recover Deleted Data
SQLite databases do not immediately remove deleted data but mark it as free space.
```sql
PRAGMA page_size;
PRAGMA integrity_check;
PRAGMA freelist_count;
```
To recover deleted records, forensic analysts can use:
```sql
SELECT * FROM sqlite_master;
SELECT * FROM deleted_table;
```

### B. Recovering SQLite Data Using Forensic Tools
- **sqlite3** – Command-line tool to query SQLite databases.
- **Autopsy** – Extracts and analyzes SQLite databases.
- **SQLite Forensic Explorer** – Recovers and investigates deleted SQLite records.
- **Undark** – Analyzes and recovers deleted data from SQLite databases.
- **Forensic Browser for SQLite** – Specialized for forensic analysis of SQLite databases.

### C. Hex Analysis of SQLite Databases
Using a hex editor, analysts can manually extract deleted data:
1. Open the database file in a hex editor (HxD, WinHex, or Hex Fiend).
2. Look for patterns of deleted data (`SQLite format 3` header).
3. Extract and reconstruct records manually.

## 4. Extracting Artifacts from SQLite Databases
To extract artifacts like browsing history, messages, and credentials:
```cmd
sqlite3 "C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default\History" "SELECT url, visit_count FROM urls ORDER BY visit_count DESC;"
```
Example for recovering WhatsApp messages:
```sql
SELECT key_remote_jid, data, timestamp FROM messages;
```

## 5. Tools for Carving SQLite Database Files
- **DB Browser for SQLite** – GUI-based SQLite viewer and editor.
- **Forensic Toolkit (FTK Imager)** – Extracts and analyzes SQLite files.
- **SQLCarve** – Recovers deleted SQLite records.
- **Belkasoft Evidence Center** – Extracts forensic artifacts from SQLite.

## Conclusion
Carving SQLite database files is crucial in forensic investigations to recover deleted data, extract user activity logs, and analyze digital artifacts. By using specialized tools and techniques, forensic experts can retrieve valuable information from SQLite-based applications.

---
✅ **Always ensure ethical and legal considerations when analyzing SQLite database files.**
