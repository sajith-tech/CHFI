
# Identifying the Traces of TOR Browser During Investigation

## What is the TOR Browser?
The **Tor (The Onion Router) Browser** is a privacy-focused web browser that allows users to access the internet anonymously. It routes traffic through a decentralized network of nodes, making it difficult to trace users.

## Why Investigate TOR Browser Usage?
- Cybercriminals use TOR for illegal activities like drug trafficking, hacking, and dark web access.
- Investigators need to find traces of TOR usage on a suspect’s system to gather digital evidence.

## Where to Look for TOR Traces?

### 1. Installed Files and Directories
TOR does not require installation, but investigators can find traces in:
- **Windows:** `C:\Users\Username\Downloads\Tor Browser\`
- **Linux/macOS:** `/home/username/tor-browser/`
- Look for files like:
  - `firefox.exe` (modified for TOR)
  - `tor.exe`
  - `torrc` (TOR configuration file)

### 2. Browser Artifacts
- **Browsing history:** TOR deletes history after closing, but forensic tools may recover data.
- **Bookmarks & Cookies:** Located in `Tor Browser/Data/Browser/profile.default/`
- **Cache Files:** Check memory dumps and pagefile.sys for cached web pages.

### 3. System Logs and Registry Entries (Windows)
- Registry traces:
  ```plaintext
  HKEY_CURRENT_USER\Software\Tor Project
  ```
- Prefetch files: Look for `tor.exe-XXXXXXXX.pf` in `C:\Windows\Prefetch`
- Recent files: Search `C:\Users\Username\AppData\Local\`

### 4. Network Logs
- TOR traffic has specific network patterns:
  - Connects to `*.onion` domains.
  - Uses high-entropy encrypted traffic.
  - TOR relays typically use ports `9001`, `9030`, `9150`, or `9151`.

- Use **Wireshark** to detect TOR traffic:
  ```bash
  tcp.port == 9001 || tcp.port == 9150
  ```

### 5. Memory Analysis
- Capture RAM using **Volatility** or **FTK Imager**.
- Extract **running processes**:
  ```bash
  volatility -f memory.dmp --profile=Win10x64 pslist | grep tor
  ```

### 6. DNS and Proxy Settings
- Check **DNS cache**:
  ```bash
  ipconfig /displaydns | findstr ".onion"
  ```
- Examine **proxy settings** in browsers and system configurations.

## Tools for TOR Browser Forensics
- **Autopsy / Sleuth Kit** - Disk analysis.
- **Wireshark** - Network packet analysis.
- **Volatility** - Memory forensics.
- **Tor Browser Analyzer** - Extracts TOR artifacts.

## Conclusion
Even though TOR is designed for anonymity, forensic traces can still be found in system logs, memory, and network traffic. Investigators can use forensic tools to identify TOR usage and analyze suspect activities.
```
