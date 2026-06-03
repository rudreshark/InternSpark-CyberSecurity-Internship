# InternSpark Cybersecurity Internship - Task 3: Network Traffic Analysis & Packet Inspection

## 📋 Project Overview

This repository contains a comprehensive network traffic analysis assessment conducted as part of the **InternSpark Internship Program**. Task 3 focuses on capturing, analyzing, and interpreting network packets using industry-standard network analysis tools to identify protocols, anomalies, and suspicious traffic patterns.

### Project Details
- **Prepared By:** Rudresha RK
- **Institution:** InternSpark Internship
- **Task:** Task 3 - Network Traffic Analysis & Packet Inspection
- **Date:** June 2026
- **Classification:** CONFIDENTIAL / INTERNAL ONLY

---

## 🎯 Task 3 Objectives

✅ Capture live network traffic across multiple protocols (HTTP, DNS, TCP)  
✅ Analyze TCP handshakes and connection establishment processes  
✅ Examine packet structure, headers, and protocol-specific fields  
✅ Identify and flag suspicious, malformed, or anomalous packets  
✅ Detect unusual traffic patterns indicating potential security threats  
✅ Document findings with packet-level analysis and forensic evidence  
✅ Generate professional traffic analysis reports with screenshots  

---

## 📊 Assessment Details

| Category | Details |
|----------|---------|
| **Target Network** | Isolated lab network (VirtualBox Host-Only / Virtual Switch) |
| **Testing Environment** | Kali Linux / Linux workstation with Wireshark |
| **Tools Used** | Wireshark, tcpdump, Tshark |
| **Protocols Analyzed** | HTTP, HTTPS, DNS, TCP, IP, ARP, ICMP |
| **Assessment Type** | Network Traffic Capture & Analysis |

---

## 📡 Network Protocol Analysis Guide

### TCP (Transmission Control Protocol) - Three-Way Handshake

**Step 1: SYN** → **Step 2: SYN-ACK** → **Step 3: ACK**

| Phase | Source | Dest | Flags | Purpose |
|-------|--------|------|-------|---------|
| 1 | Client | Server | SYN | Request connection |
| 2 | Server | Client | SYN-ACK | Accept connection |
| 3 | Client | Server | ACK | Confirm connection |

### DNS (Domain Name System) Query Types

| Type | Purpose |
|------|---------|
| **A** | IPv4 address resolution |
| **AAAA** | IPv6 address resolution |
| **MX** | Mail exchange server |
| **CNAME** | Canonical name alias |

### HTTP Response Codes

| Code | Meaning |
|------|---------|
| **2xx** | Success |
| **3xx** | Redirection |
| **4xx** | Client Error |
| **5xx** | Server Error |

---

## 🔍 Wireshark Usage Guide

### Installation
```bash
sudo apt-get install wireshark tshark
```

### Display Filters
```
http              # HTTP traffic only
dns               # DNS traffic only
tcp.flags.syn==1  # SYN packets only
tcp.flags.fin==1  # FIN packets only
tcp.flags.rst==1  # RST packets only
ip.addr==192.168.1.1  # Specific IP
```

### Analyzing Traffic
1. **TCP Handshake**: Apply filter `tcp.handshake`
2. **DNS Queries**: Apply filter `dns`
3. **HTTP Requests**: Apply filter `http` then Follow Stream

---

## ⚠️ Suspicious Indicators

❌ SYN flood attacks  
❌ DNS tunneling  
❌ Data exfiltration  
❌ Port scanning  
❌ Malformed packets  
❌ Unusual port combinations  

---

## 📁 Repository Structure

```
task-3/
├── README.md
├── captures/
│   ├── full_capture.pcap
│   ├── tcp_handshake.pcap
│   ├── dns_queries.pcap
│   └── http_traffic.pcap
├── screenshots/
│   ├── tcp_analysis/
│   ├── dns_analysis/
│   ├── http_analysis/
│   └── suspicious_traffic/
└── analysis/
    ├── traffic_analysis_report.txt
    ├── protocol_statistics.txt
    └── recommendations.txt
```

---

## 👤 Author Information

**Prepared By:** Rudresha RK  
**Program:** InternSpark Cybersecurity Internship  
**Date:** June 2026  

---

**Status:** Ready for Submission
