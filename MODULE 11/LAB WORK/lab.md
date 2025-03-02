
# Detect TOR Browser Activity and Examine RAM Dumps for TOR Artifacts

## 1. Introduction
The **TOR (The Onion Router) Browser** allows users to browse anonymously by encrypting traffic and routing it through multiple relays. However, forensic investigators can still detect traces of TOR activity and extract artifacts from RAM dumps.

This guide provides **open-source** methods to:
- Detect **TOR activity** on a system.
- Analyze **network logs** for TOR traffic.
- Examine **RAM dumps** to extract TOR artifacts.

---

## 2. Detecting TOR Browser Activity

### **2.1 Checking Running Processes**
Use terminal commands to find active TOR processes.

#### **Windows (PowerShell/CMD)**
```powershell
tasklist | findstr /i "tor firefox"
wmic process where "name like '%tor%'" get name, processid
```

#### **Linux/macOS**
```bash
ps aux | grep -i tor
pgrep tor
```

### **2.2 Checking Installed Files**
TOR Browser is typically **portable** and does not require installation. Look in common directories:

#### **Windows**
```powershell
dir "C:\Users\*\Desktop\Tor Browser" /s /b
dir "C:\Users\*\Downloads\Tor Browser" /s /b
```

#### **Linux**
```bash
find /home -type d -name "tor-browser*"
```

---

## 3. Analyzing Network Traffic for TOR Activity

TOR communicates over specific ports. Check for TOR-related connections.

### **3.1 Identify Active TOR Connections**
#### **Windows**
```powershell
netstat -ano | findstr "9001 9030 9150 9151"
```

#### **Linux/macOS**
```bash
netstat -tulnp | grep -E "9001|9030|9150|9151"
```

### **3.2 Using Wireshark to Capture TOR Traffic**
- Open Wireshark and apply this filter:
  ```
  tcp.port == 9001 || tcp.port == 9030 || tcp.port == 9150 || tcp.port == 9151
  ```
- Look for **encrypted traffic** to TOR entry nodes.

### **3.3 Checking DNS Cache for `.onion` Domains**
#### **Windows**
```powershell
ipconfig /displaydns | findstr ".onion"
```

#### **Linux/macOS**
```bash
grep ".onion" /var/log/syslog
```

---

## 4. Examining RAM Dumps for TOR Browser Artifacts

### **4.1 Acquiring a RAM Dump**
Use **open-source tools** to dump system memory:

#### **Windows - Dump with DumpIt**
1. Download **DumpIt**: [https://download.cnet.com/DumpIt/](https://download.cnet.com/DumpIt/)
2. Run as administrator, and it will create a memory dump.

#### **Linux - Dump with LiME**
```bash
sudo apt install linux-tools-common linux-tools-generic
sudo modprobe lime
lime -o /tmp/memory.dmp -f raw
```

---

### **4.2 Analyzing RAM Dump with Volatility**
Use **Volatility**, an open-source memory forensics framework.

#### **Find Running TOR Processes**
```bash
volatility -f memory.dmp --profile=Win10x64 pslist | grep tor
```

#### **Extract TOR Browser URLs**
```bash
volatility -f memory.dmp --profile=Win10x64 strings | grep ".onion"
```

#### **Recover Open TOR Tabs**
```bash
volatility -f memory.dmp --profile=Win10x64 dumpfiles -r "places.sqlite" -D output/
```
Open `places.sqlite` in **SQLite Browser** to see visited `.onion` sites.

---

## 5. Extracting TOR Artifacts from Memory

### **5.1 Searching for TOR Configuration Files**
TOR uses a configuration file named **torrc**.

```bash
strings memory.dmp | grep -i "torrc"
```

### **5.2 Recovering User Activity**
Search for **recent downloads**:
```bash
strings memory.dmp | grep -i "Downloads"
```
Extract **chat messages** from `.onion` sites:
```bash
strings memory.dmp | grep -i "chat"
```

---

## 6. Conclusion
By detecting **running processes, network activity, and memory artifacts**, forensic investigators can trace TOR usage. **Volatility, netstat, and Wireshark** are powerful **open-source** tools for this analysis.

---
## **7. Tools Used**
✅ **Volatility** - RAM analysis  
✅ **Wireshark** - Network traffic monitoring  
✅ **DumpIt / LiME** - Memory acquisition  
✅ **SQLite Browser** - Extracting `.onion` history  

**👉 Practice these techniques in a safe lab environment!**
```
