
# TOR Browser Forensics

## What is the TOR Browser?
The **TOR (The Onion Router) Browser** is a privacy-focused web browser that anonymizes internet traffic using a network of relays. It is commonly used to access the dark web, bypass censorship, and maintain anonymity.

## Why is TOR Browser Forensics Important?
- Cybercriminals use TOR to hide their activities, making forensic analysis crucial.
- Investigators need to uncover traces of TOR usage to link users to illegal activities.

## 1. Locating TOR Browser on a System
TOR is often run as a **portable application**, meaning it does not require installation. Common locations include:
- **Windows:**  
  - `C:\Users\Username\Downloads\Tor Browser\`
  - `C:\Users\Username\Desktop\Tor Browser\`
- **Linux/macOS:**  
  - `/home/username/tor-browser/`
  - `/Applications/Tor Browser.app/`

Check for **files and directories** like:
- `tor.exe` (Windows) / `tor` (Linux)
- `torrc` (Configuration file)
- `firefox.exe` (Modified Firefox used by TOR)

## 2. Identifying TOR Browser Artifacts

### **2.1 System Artifacts (Windows)**
- **Registry Entries:**
  ```plaintext
  HKEY_CURRENT_USER\Software\Tor Project
  ```
- **Prefetch Files:** Look for `tor.exe-XXXXXXXX.pf` in `C:\Windows\Prefetch`
- **Recent Files:** Check `C:\Users\Username\AppData\Local\`

### **2.2 Browser Artifacts**
- **History & Bookmarks**:  
  - `Tor Browser/Data/Browser/profile.default/places.sqlite`
- **Cookies & Cache**:  
  - `Tor Browser/Data/Browser/profile.default/cookies.sqlite`
- **Downloaded Files**:  
  - `Tor Browser/Data/Browser/profile.default/downloads.json`

### **2.3 Network Artifacts**
- **Ports Used by TOR:**  
  - `9001`, `9030`, `9150`, `9151`
- **TOR Entry Node IPs:**  
  - Check `torrc` file for manually configured entry nodes.
- **Network Traffic Analysis using Wireshark:**  
  ```bash
  tcp.port == 9001 || tcp.port == 9150
  ```

### **2.4 Memory Artifacts**
Capture RAM using **Volatility** or **FTK Imager** and extract running TOR processes:
```bash
volatility -f memory.dmp --profile=Win10x64 pslist | grep tor
```
Check for **TOR-related strings** in memory dumps:
```bash
strings memory.dmp | grep ".onion"
```

## 3. Investigating TOR Usage
### **3.1 Checking DNS and Proxy Settings**
- **Check DNS Cache (Windows):**
  ```bash
  ipconfig /displaydns | findstr ".onion"
  ```
- **Check Proxy Settings (Linux):**
  ```bash
  cat /etc/proxychains.conf
  ```

### **3.2 Extracting Dark Web Access Logs**
- Check **logins.json** for saved credentials.
- Analyze `places.sqlite` for visited `.onion` websites.
- Look for `.onion` URLs in system logs.

## 4. Tools for TOR Browser Forensics
- **Autopsy / Sleuth Kit** - Disk analysis.
- **Wireshark** - Network packet analysis.
- **Volatility** - Memory forensics.
- **Tor Browser Analyzer** - Extracts TOR artifacts.
- **ExifTool** - Extract metadata from TOR-downloaded files.

## 5. Conclusion
Despite its anonymity features, TOR Browser leaves forensic traces in system files, memory, and network logs. Investigators can use forensic tools to uncover evidence of TOR usage and link it to specific activities.

```
