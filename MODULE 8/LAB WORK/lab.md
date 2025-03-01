# Network Forensics Lab Guide

## Lab 1: Identify and Investigate Network Attacks

### Objective
This lab focuses on identifying and investigating network attacks using open-source tools.

### Tools Required
- **Wireshark** (Packet capture and analysis)
- **Tcpdump** (Command-line packet capture tool)
- **Snort** (Intrusion Detection System)
- **Metasploit** (For simulating attacks)
- **Kali Linux** (For running tools)

### Steps
#### 1. Capturing Network Traffic
   - Open Wireshark and start capturing packets.
   - Use `tcpdump -i eth0 -w capture.pcap` to capture traffic from a specific interface.

#### 2. Simulating a Network Attack
   - Use Metasploit to launch a simulated attack:
     ```bash
     msfconsole
     use auxiliary/dos/tcp/synflood
     set RHOST <target-IP>
     exploit
     ```

#### 3. Detecting the Attack
   - Open Wireshark and filter for TCP SYN flood:
     ```
     tcp.flags.syn == 1 && tcp.flags.ack == 0
     ```
   - Analyze packet timestamps and volume to confirm the attack.

#### 4. Using Snort for Detection
   - Start Snort in packet logging mode:
     ```bash
     snort -i eth0 -l /var/log/snort -c /etc/snort/snort.conf
     ```
   - Check logs for alerts indicating a SYN flood attack.

#### 5. Investigating Logs
   - Review system logs in `/var/log/syslog` for unusual activity.
   - Check firewall logs using `sudo cat /var/log/ufw.log`.

### Key Takeaways
- **Recognizing attack patterns**: SYN floods, brute force, MITM.
- **Using Wireshark for analysis**: Packet dissection and filtering.
- **IDS/IPS for monitoring**: Snort detects and alerts on attacks.

---

## Lab 2: Analyze Network Traffic for Artifacts

### Objective
This lab helps analyze network traffic to identify artifacts related to cybersecurity incidents.

### Tools Required
- **Wireshark**
- **NetworkMiner**
- **Zeek (Bro)**
- **Tshark**

### Steps
#### 1. Capturing Network Traffic
   - Start capturing packets using Wireshark.
   - Use Tshark for command-line packet capture:
     ```bash
     tshark -i eth0 -w traffic.pcap
     ```

#### 2. Extracting Network Artifacts
   - Identify suspicious connections:
     ```
     ip.dst == <suspicious-IP>
     ```
   - Check for large data transfers or anomalies.

#### 3. Using NetworkMiner for Artifact Extraction
   - Open captured packets in NetworkMiner.
   - Extract files, images, credentials, and DNS queries.

#### 4. Detecting Malicious Traffic with Zeek
   - Analyze traffic logs with Zeek:
     ```bash
     zeek -r traffic.pcap
     cat conn.log
     ```
   - Identify unauthorized access or suspicious domain requests.

### Key Takeaways
- **Packet analysis**: Identifying malicious activities.
- **Artifact extraction**: Recovering files, credentials, and indicators of compromise.
- **Threat detection**: Analyzing DNS, HTTP, and TLS traffic.

## Conclusion
These labs provide hands-on experience in network forensics, covering attack detection, investigation, and artifact analysis using open-source tools.
