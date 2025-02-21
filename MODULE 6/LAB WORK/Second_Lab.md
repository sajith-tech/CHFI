# Examine Forensic Artifacts from Web Browsers

## Introduction
Web browser forensics involves extracting and analyzing artifacts left by users, such as history, cookies, cache, and session data. These artifacts provide crucial insights into browsing behavior, downloaded files, and authentication details.

## Important Browser Artifacts
| Artifact | Location | Purpose |
|----------|---------|---------|
| History | `AppData\Local\<Browser>\User Data\Default\History` | Tracks visited websites |
| Cookies | `AppData\Local\<Browser>\User Data\Default\Cookies` | Stores user preferences and session data |
| Cache | `AppData\Local\<Browser>\User Data\Default\Cache` | Contains temporary stored web data |
| Downloads | `AppData\Local\<Browser>\User Data\Default\Downloads` | Lists downloaded files |
| Autofill | `AppData\Local\<Browser>\User Data\Default\Web Data` | Stores form data and saved credentials |

## Tools for Browser Forensics
- **BrowserHistoryView** (Windows) – Extracts history from multiple browsers.
- **WebBrowserPassView** – Recovers saved passwords.
- **sqlitebrowser** – Analyzes SQLite database files.
- **ChromeForensics** – Extracts artifacts from Chrome.
- **MozillaCacheView** – Analyzes Firefox cache files.

## Extracting Browser History
### Using BrowserHistoryView
1. Download and run **BrowserHistoryView**.
2. It will automatically scan and display history from installed browsers.
3. Export the results for analysis.

### Using SQLite to Analyze History Manually
1. Locate the history database:
   ```
   C:\Users\<Username>\AppData\Local\Google\Chrome\User Data\Default\History
   ```
2. Open with SQLite Browser:
   ```sql
   SELECT url, title, visit_count, last_visit_time FROM urls ORDER BY last_visit_time DESC;
   ```
3. Analyze timestamps and URL visits.

## Extracting Cookies
1. Locate the cookies database:
   ```
   C:\Users\<Username>\AppData\Local\Google\Chrome\User Data\Default\Cookies
   ```
2. Open using SQLite Browser and run:
   ```sql
   SELECT host_key, name, value FROM cookies;
   ```
3. Review session data and authentication tokens.

## Extracting Download History
1. Locate the downloads database:
   ```
   C:\Users\<Username>\AppData\Local\Google\Chrome\User Data\Default\Downloads
   ```
2. Open using SQLite Browser:
   ```sql
   SELECT target_path, tab_url, total_bytes FROM downloads;
   ```
3. Review downloaded file details and sources.

## Extracting Saved Passwords
1. Use **WebBrowserPassView** to recover stored credentials.
2. For Chrome, extract credentials manually:
   ```sql
   SELECT origin_url, username_value, password_value FROM logins;
   ```
3. Chrome passwords are encrypted and require decryption tools.

## Conclusion
Web browser forensics provides valuable evidence related to user activities, online behaviors, and stored credentials. Using tools like SQLite, BrowserHistoryView, and WebBrowserPassView, forensic investigators can extract and analyze browsing artifacts effectively.

---
✅ **Always ensure legal authorization before extracting browser artifacts.**
