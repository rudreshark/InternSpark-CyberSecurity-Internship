# InternSpark Cybersecurity Internship - Task 1: Active Reconnaissance & Vulnerability Scanning

## 📋 Project Overview

This repository contains a comprehensive active reconnaissance and vulnerability assessment conducted as part of the **InternSpark Internship Program**. Task 1 focuses on host discovery, service enumeration, and identifying security vulnerabilities using industry-standard tools.

### Project Details
- **Prepared By:** Rudresha RK
- **Institution:** InternSpark Internship
- **Task:** Task 1 - Active Reconnaissance & Vulnerability Scanning
- **Date:** June 2026
- **Classification:** CONFIDENTIAL / INTERNAL ONLY

---

## 🎯 Task 1 Objectives

✅ Perform host discovery and network enumeration  
✅ Identify active services and open ports  
✅ Detect service versions and software  
✅ Scan for web server vulnerabilities  
✅ Identify misconfigurations and weak services  
✅ Cross-reference findings with CVE databases  
✅ Prioritize vulnerabilities by severity  
✅ Generate comprehensive remediation recommendations  

---

## 📊 Assessment Details

| Category | Details |
|----------|---------|
| **Target System** | Metasploitable 2 (Linux) |
| **Target Network** | VirtualBox Host-Only (192.168.56.0/24) |
| **Testing Environment** | Kali Linux / Linux workstation |
| **Tools Used** | Nmap, Nikto, Netstat |
| **Protocols Scanned** | TCP, UDP |
| **Assessment Type** | Active Reconnaissance & Vulnerability Scanning |

---

## 🔍 Reconnaissance Methodology

### Phase 1: Host Discovery

**Objective:** Identify active hosts on the target network

```bash
# ICMP Echo Request (Ping Sweep)
nmap -sn 192.168.56.0/24

# ARP Scan
nmap -PR 192.168.56.0/24

# TCP SYN Ping
nmap -PS 192.168.56.0/24
```

### Phase 2: Port Enumeration

**Objective:** Identify open, closed, and filtered ports

```bash
# TCP Connect Scan (Most reliable)
nmap -sT 192.168.56.101

# TCP SYN Scan (Stealth scan)
nmap -sS 192.168.56.101

# UDP Scan
nmap -sU 192.168.56.101

# All ports scan
nmap -p- 192.168.56.101

# Specific port range
nmap -p 1-1000 192.168.56.101
```

### Phase 3: Service Version Detection

**Objective:** Identify running services and software versions

```bash
# Service version detection
nmap -sV 192.168.56.101

# OS fingerprinting
nmap -O 192.168.56.101

# Aggressive scan (includes OS, version, script, traceroute)
nmap -A 192.168.56.101

# Script scanning
nmap -sC 192.168.56.101
```

---

## 📊 Nmap Usage Guide

### Command Structure
```
nmap [Scan Type] [Options] [Target]
```

### Scan Types

| Scan Type | Flag | Description |
|-----------|------|-------------|
| TCP Connect | -sT | Full TCP connection (reliable, logged) |
| TCP SYN | -sS | Half-open scan (stealthy) |
| UDP | -sU | UDP port scan |
| FIN | -sF | FIN packets only |
| NULL | -sN | No flags set |
| XMAS | -sX | FIN, PSH, URG flags |
| ACK | -sA | Firewall mapping |
| Ping | -sn | Host discovery only |

### Detection Options

| Option | Description |
|--------|-------------|
| -sV | Service/version detection |
| -O | OS detection |
| -A | Aggressive (OS, version, script, traceroute) |
| -sC | Run default scripts |
| --script | Run specific script |

### Output Formats

| Format | Flag |
|--------|------|
| Normal | -oN filename |
| Grepable | -oG filename |
| XML | -oX filename |
| All formats | -oA filename |

### Common Usage Examples

```bash
# Basic scan
nmap 192.168.56.101

# Comprehensive scan
nmap -A -p- 192.168.56.101

# Service detection with scripts
nmap -sV -sC 192.168.56.101

# OS detection
nmap -O 192.168.56.101

# Aggressive scan with output
nmap -A -T4 -oN scan_results.txt 192.168.56.101

# UDP service discovery
nmap -sU -p 53,67,68,123 192.168.56.101

# Timing templates (T0-T5)
nmap -T4 192.168.56.101
```

---

## 🔎 Vulnerability Scanning with Nikto

### Overview
Nikto is a web server scanner that identifies:
- Outdated software versions
- Dangerous files and CGI scripts
- Misconfigurations
- HTTP headers issues

### Installation
```bash
sudo apt-get install nikto
```

### Basic Syntax
```
nikto -h target_url [options]
```

### Common Usage

```bash
# Basic web server scan
nikto -h http://192.168.56.101

# Specify port
nikto -h http://192.168.56.101:80

# Save output
nikto -h http://192.168.56.101 -o nikto_report.html

# Verbose output
nikto -h http://192.168.56.101 -v

# Use specific port
nikto -h 192.168.56.101 -p 8080

# Scan multiple ports
nikto -h 192.168.56.101 -p 80,443,8080
```

### Output Interpretation

```
[+] Server: Apache/2.2.15
[+] Detected: Apache 2.2.15
[!] OSVDB-# - Remote: Vulnerable to [Vulnerability]
[?] Questionable: Check if this is an issue
```

---

## 🚨 Common Vulnerabilities Found

### Service Vulnerabilities

#### 1. **FTP (Port 21)**
```
Service: vsftpd 2.3.4
Vulnerability: Backdoor in vsftpd 2.3.4
CVE: CVE-2011-2523
Severity: CRITICAL
Details: Remote code execution via :) smiley face sequence
```

#### 2. **SSH (Port 22)**
```
Service: OpenSSH 4.7p1
Vulnerability: Protocol weakness
Severity: LOW-MEDIUM
Details: Supports weak cipher suites
```

#### 3. **Telnet (Port 23)**
```
Service: Linux Telnet
Vulnerability: Unencrypted communication
CVE: CWE-295
Severity: HIGH
Details: Credentials transmitted in plain text
```

#### 4. **SMTP (Port 25)**
```
Service: Postfix
Vulnerability: Open relay misconfiguration
Severity: MEDIUM
Details: Can relay emails
```

#### 5. **DNS (Port 53)**
```
Service: BIND 9.x
Vulnerability: DNS amplification attack
Severity: MEDIUM
Details: Can be used for DDoS amplification
```

#### 6. **HTTP (Port 80)**
```
Service: Apache 2.2.x
Vulnerabilities: 
- Outdated version
- Directory listing enabled
- Default pages present
Severity: MEDIUM-HIGH
```

#### 7. **Samba (Port 139/445)**
```
Service: Samba 3.x
Vulnerability: Remote Code Execution
CVE: CVE-2007-6015 (or similar)
Severity: CRITICAL
Details: Unauthenticated file access
```

#### 8. **MySQL (Port 3306)**
```
Service: MySQL 5.x
Vulnerability: No password on root account
Severity: CRITICAL
Details: Allows unauthenticated database access
```

---

## 📈 Vulnerability Assessment Report

### Executive Summary
```
Assessment Date: June 3, 2026
Target: Metasploitable 2 (192.168.56.101)
Total Vulnerabilities: 6
- CRITICAL: 2
- HIGH: 3
- MEDIUM: 1
```

### Vulnerability Breakdown

#### CRITICAL Vulnerabilities (Fix Immediately)
```
1. FTP Backdoor (vsftpd 2.3.4)
   - Port: 21
   - CVE: CVE-2011-2523
   - Impact: Remote Code Execution
   - Fix: Update to patched version

2. Samba RCE (Samba 3.x)
   - Port: 139/445
   - CVE: CVE-2007-6015
   - Impact: Unauthenticated RCE
   - Fix: Apply patches, disable if not needed
```

#### HIGH Vulnerabilities (Fix Soon)
```
1. Telnet Service (Unencrypted)
   - Port: 23
   - Issue: Plain text credential transmission
   - Fix: Disable Telnet, use SSH only

2. MySQL No Password
   - Port: 3306
   - Issue: Root account without password
   - Fix: Set strong password, restrict access

3. HTTP Directory Listing
   - Port: 80
   - Issue: Directories are browsable
   - Fix: Disable directory listing
```

#### MEDIUM Vulnerabilities (Fix When Possible)
```
1. phpinfo.php Exposed
   - Port: 80
   - Issue: Server information disclosure
   - Fix: Remove phpinfo.php or restrict access
```

---

## 🔧 Port Reference Guide

| Port | Service | Protocol | Risk Level |
|------|---------|----------|-----------|
| 21 | FTP | TCP | CRITICAL |
| 22 | SSH | TCP | LOW |
| 23 | Telnet | TCP | CRITICAL |
| 25 | SMTP | TCP | MEDIUM |
| 53 | DNS | TCP/UDP | MEDIUM |
| 80 | HTTP | TCP | MEDIUM-HIGH |
| 111 | rpcbind | TCP/UDP | HIGH |
| 139 | Samba | TCP | CRITICAL |
| 445 | Samba | TCP | CRITICAL |
| 3306 | MySQL | TCP | CRITICAL |
| 3632 | distcc | TCP | HIGH |
| 5432 | PostgreSQL | TCP | MEDIUM |
| 5900 | VNC | TCP | MEDIUM |

---

## 📋 Remediation Recommendations

### Immediate Actions (0-24 hours)

```
1. Disable FTP service
   - Disable vsftpd daemon
   - Use SFTP/SCP instead
   - Rationale: Critical RCE vulnerability

2. Patch Samba service
   - Apply security patches
   - Or disable if not required
   - Rationale: Unauthenticated RCE

3. Disable Telnet
   - Shutdown telnet daemon
   - Use SSH only
   - Rationale: Plaintext credentials
```

### Short-Term Actions (1-7 days)

```
1. Secure MySQL
   - Set root password
   - Restrict network access
   - Create minimal privilege accounts
   - Rationale: Unauthorized database access

2. Configure HTTP properly
   - Disable directory listing
   - Remove test files (phpinfo.php)
   - Configure security headers
   - Rationale: Information disclosure

3. Update SSH configuration
   - Disable weak ciphers
   - Implement key-based auth only
   - Rationale: Strengthen authentication
```

### Long-Term Actions (1-4 weeks)

```
1. System patching policy
   - Implement regular patches
   - Set up security advisories
   - Test patches before deployment
   - Rationale: Preventive maintenance

2. Network segmentation
   - Implement firewall rules
   - Restrict port access
   - Implement IDS/IPS
   - Rationale: Defense in depth

3. Monitoring & alerting
   - Enable system logging
   - Monitor suspicious activities
   - Set up SIEM solution
   - Rationale: Early threat detection
```

---

## 🛡️ Security Hardening Checklist

- [ ] Disable unnecessary services
- [ ] Update all software to latest patches
- [ ] Change default credentials
- [ ] Implement firewall rules
- [ ] Enable security logging
- [ ] Configure SELinux/AppArmor
- [ ] Implement strong password policy
- [ ] Enable SSH key-based authentication
- [ ] Disable remote root login
- [ ] Set up SIEM monitoring
- [ ] Conduct regular vulnerability scans
- [ ] Perform penetration testing

---

## 🔐 CVE Cross-Reference

### CVE-2011-2523 (vsftpd Backdoor)
```
Product: vsftpd 2.3.4
Type: Remote Code Execution
Description: Allows remote attacker to execute commands
CVSS: 9.8 (Critical)
Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-2523
```

### CVE-2007-6015 (Samba RCE)
```
Product: Samba 3.0.0 - 3.0.25rc3
Type: Remote Code Execution
Description: Arbitrary code execution via crafted requests
CVSS: 9.3 (Critical)
Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6015
```

---

## 📁 Repository Structure

```
task-1/
├── TASK1_README.md
├── scans/
│   ├── nmap_host_discovery.txt
│   ├── nmap_port_scan.txt
│   ├── nmap_service_detection.txt
│   ├── nmap_os_detection.txt
│   └── nikto_web_scan.html
├── screenshots/
│   ├── nmap_output.png
│   ├── nikto_results.png
│   └── vulnerability_summary.png
├── analysis/
│   ├── vulnerability_assessment_report.txt
│   ├── remediation_plan.txt
│   └── cve_cross_reference.txt
└── tools/
    └── scan_scripts.sh
```

---

## 📚 Tools & Documentation

### Nmap Resources
- [Official Nmap Book](https://nmap.org/book/)
- [Nmap Reference Guide](https://nmap.org/docs.html)
- [Nmap NSE Scripts](https://nmap.org/nsedoc/)

### Nikto Resources
- [Nikto Project](https://cirt.net/Nikto2)
- [Nikto GitHub](https://github.com/sullo/nikto)

### Vulnerability Databases
- [CVE MITRE](https://cve.mitre.org/)
- [NVD - NIST](https://nvd.nist.gov/)
- [Exploit Database](https://www.exploit-db.com/)

---

## ⚠️ Important Notes

### Ethical Considerations
- ✅ Only scan authorized targets
- ✅ Document all activities
- ✅ Follow responsible disclosure
- ✅ Maintain confidentiality
- ✅ Comply with legal requirements

### Best Practices
- Use consistent naming conventions
- Document all findings
- Take screenshots for evidence
- Keep scan timestamps
- Archive all reports
- Follow up on recommendations

---

## 👤 Author Information

**Prepared By:** Rudresha RK  
**Program:** InternSpark Cybersecurity Internship  
**Date:** June 2026  

---

**Status:** Ready for Submission
