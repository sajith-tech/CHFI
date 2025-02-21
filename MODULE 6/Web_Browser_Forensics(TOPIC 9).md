# Web Browser Forensics

## Introduction
Web browser forensics involves the investigation of browser artifacts such as history, cache, cookies, bookmarks, and session data. Browsers store significant user activity data, making them crucial for forensic investigations.

## 1. Importance of Web Browser Forensics
- **User Activity Tracking** – Identifies visited websites, search queries, and downloads.
- **Credential Recovery** – Extracts saved passwords and authentication tokens.
- **Session and Cookie Analysis** – Finds active session tokens for user accounts.
- **Cache and Artifact Recovery** – Recovers cached images, files, and browsing history.

## 2. Common Web Browsers and Storage Locations
Web browsers store forensic artifacts in different locations based on the operating system.

### Google Chrome
#### Windows:
```
C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default\
```
#### Linux:
```
/home/<username>/.config/google-chrome/Default/
```
#### macOS:
```
/Users/<username>/Library/Application Support/Google/Chrome/Default/
```

### Mozilla Firefox
#### Windows:
```
C:\Users\<username>\AppData\Roaming\Mozilla\Firefox\Profiles\<profile-name>\
```
#### Linux:
```
/home/<username>/.mozilla/firefox/<profile-name>/
```
#### macOS:
```
/Users/<username>/Library/Application Support/Firefox/Profiles/<profile-name>/
```

### Microsoft Edge
```
C:\Users\<username>\AppData\Local\Microsoft\Edge\User Data\Default\
```

## 3. Key Browser Artifacts
- **History Database (`History` or `places.sqlite`)** – Stores visited URLs and timestamps.
- **Cookies (`Cookies` or `cookies.sqlite`)** – Contains authentication tokens and session data.
- **Cache (`Cache` or `cache2/entries/`)** – Stores temporary website data, including images and scripts.
- **Download Records (`History` or `downloads.json`)** – Lists downloaded files and paths.
- **Saved Passwords (`Login Data` or `logins.json`)** – Stores usernames and encrypted passwords.
- **Form Autofill Data (`Web Data` or `formhistory.sqlite`)** – Stores autofill form data like names, addresses, and credit card details.

## 4. Extracting Data from Web Browsers
### A. Extracting Browsing History (Google Chrome)
Google Chrome stores browsing history in an SQLite database:
```cmd
sqlite3 "C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default\History" "SELECT url, title, visit_count, last_visit_time FROM urls ORDER BY last_visit_time DESC;"
```

### B. Extracting Cookies
```cmd
sqlite3 "C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default\Cookies" "SELECT host_key, name, value FROM cookies;"
```

### C. Recovering Cache Files
Extract cached files using forensic tools like FTK Imager or manually browse the cache folder.
```cmd
strings "C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default\Cache\"
```

### D. Extracting Saved Passwords (Encrypted)
Google Chrome stores passwords in an encrypted format:
```cmd
sqlite3 "C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default\Login Data" "SELECT origin_url, username_value, password_value FROM logins;"
```
(Use decryption tools like `Chromepass` to view decrypted passwords.)

## 5. Tools for Web Browser Forensics
- **DB Browser for SQLite** – Analyzes SQLite-based browser databases.
- **FTK Imager** – Extracts and analyzes browser cache and history.
- **Browser History Viewer** – Provides an interface for viewing browser history.
- **Hindsight** – A browser forensic analysis tool for Chrome and Edge.
- **WebCacheViewer** – Extracts and analyzes browser cache files.

## Conclusion
Web browser forensics is essential for investigating digital footprints, cybercrime cases, and user activities. By analyzing history, cache, cookies, and saved passwords, forensic experts can uncover valuable evidence for security investigations.

---
✅ **Ensure legal and ethical considerations when analyzing browser data.**
