# Linux Memory Forensics

Memory forensics is the process of analyzing a system's RAM to extract valuable information such as running processes, network connections, encryption keys, and other forensic artifacts. This is critical for detecting malware, investigating security incidents, and gathering evidence.

## 1. Acquiring Memory Dump
To analyze memory, we first need to create a memory dump. Below are some tools used for acquiring memory dumps in Linux:

### 1.1 Using `LiME` (Linux Memory Extractor)
LiME is a kernel module that allows memory acquisition:
```bash
git clone https://github.com/504ensicsLabs/LiME.git
cd LiME/src
make
sudo insmod lime.ko "path=/root/memdump.lime format=raw"
```

### 1.2 Using `avml` (Azure Volatile Memory Library)
Microsoft's AVML is another tool for memory acquisition:
```bash
wget https://github.com/microsoft/avml/releases/latest/download/avml
chmod +x avml
./avml memdump.lime
```

## 2. Analyzing Memory Dump
Once we have a memory dump, we can analyze it using `Volatility`.

### 2.1 Installing Volatility
```bash
git clone https://github.com/volatilityfoundation/volatility.git
cd volatility
python2 setup.py install
```

### 2.2 Identifying the Profile
Before running plugins, determine the system profile:
```bash
python2 volatility -f memdump.lime imageinfo
```

### 2.3 Listing Running Processes
To check the running processes at the time of the dump:
```bash
python2 volatility -f memdump.lime --profile=<profile> pslist
```

### 2.4 Checking Network Connections
To identify active network connections:
```bash
python2 volatility -f memdump.lime --profile=<profile> netscan
```

### 2.5 Extracting Command History
To recover command execution history:
```bash
python2 volatility -f memdump.lime --profile=<profile> bash
```

### 2.6 Finding Malicious Code
To check for potential malware:
```bash
python2 volatility -f memdump.lime --profile=<profile> malfind
```

## 3. Other Useful Volatility Plugins
- `filescan`: Searches for file handles in memory
- `dumpfiles`: Extracts files from memory
- `hivelist`: Lists registry hives in memory
- `shellbags`: Retrieves GUI-based file access history

## Conclusion
Memory forensics is a crucial skill in cybersecurity investigations. By using tools like `LiME`, `AVML`, and `Volatility`, forensic analysts can extract and analyze critical volatile data to uncover security incidents and malicious activities.

