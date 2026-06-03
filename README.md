# InternSpark Cybersecurity Internship - Active Reconnaissance & Vulnerability Assessment

## 📋 Project Overview

This repository contains comprehensive cybersecurity assessments conducted as part of the **InternSpark Internship Program**. The focus is on **Active Reconnaissance** and **Vulnerability Scanning** methodologies using industry-standard ethical hacking tools in a controlled, isolated lab environment.

### Project Details
- **Prepared By:** Rudresha RK
- **Institution:** InternSpark Internship
- **Date:** June 3, 2026
- **Classification:** CONFIDENTIAL / INTERNAL ONLY

---

## 🎯 Assessment Scope

### Target System
- **Platform:** Metasploitable 2 (Linux)
- **Target IP Address:** 192.168.56.101
- **Attacker Machine:** Kali Linux
- **Network Type:** VirtualBox Host-Only (192.168.56.0/24)

### Objectives
✅ Perform host discovery and confirm target availability  
✅ Enumerate open TCP ports and identify services/versions  
✅ Conduct web server vulnerability scanning  
✅ Document vulnerabilities with severity ratings and remediation steps  
✅ Produce structured security reports for technical review

---

## 🔧 Tools & Methodologies

| Tool | Purpose |
|------|---------|
| **Nmap** | Host discovery, port enumeration, service version detection, OS fingerprinting |
| **Nikto** | Web application vulnerability scanning, configuration analysis |

### Techniques Applied
- Host Discovery Ping Sweep
- TCP Port & Service Enumeration
- Aggressive OS Fingerprinting
- Web Application Security Assessment
- Vulnerability Classification & Risk Analysis

---

## 📊 Vulnerability Summary

### Vulnerability Distribution

| Severity | Count |
|----------|-------|
| **CRITICAL** | 2 |
| **HIGH** | 3 |
| **MEDIUM** | 1 |
| **TOTAL** | **6** |

### Key Findings at a Glance

| Finding ID | Vulnerability | Port | Severity | CVE Reference |
|-----------|--------------|------|----------|--------------|
| F-01 | FTP Backdoor (vsftpd 2.3.4) | 21/tcp | **CRITICAL** | CVE-2011-2523 |
| F-02 | Telnet Plaintext Protocol | 23/tcp | HIGH | N/A |
| F-03 | Samba RCE | 139, 445 | HIGH | CVE-2007-2447 |
| F-04 | MySQL No Root Password | 3306/tcp | HIGH | CWE-521 |
| F-05 | phpinfo.php Information Disclosure | 80/tcp | MEDIUM | CWE-200 |
| F-06 | UnrealIRCd Backdoor | 6667/tcp | **CRITICAL** | CVE-2010-2075 |

---

## 🔴 Critical Vulnerabilities

### F-01: FTP Backdoor (CVE-2011-2523)
- **Service:** vsftpd 2.3.4
- **Risk:** Unauthenticated root shell access via backdoor activation
- **Remediation:** Upgrade vsftpd to v3.0.x or disable FTP service

### F-06: UnrealIRCd Backdoor (CVE-2010-2075)
- **Service:** UnrealIRCd 3.2.8.1
- **Risk:** Unauthenticated remote command execution
- **Remediation:** Uninstall compromised version; reinstall from verified source

---

## 🟡 High-Severity Findings

### F-02: Telnet Service (Cleartext Protocol)
- **Impact:** Credentials exposed to network sniffing
- **Fix:** Disable Telnet; enforce SSH for all remote access

### F-03: Samba RCE (CVE-2007-2447)
- **Impact:** Unauthenticated shell command execution
- **Fix:** Upgrade Samba; restrict SMB ports via firewall

### F-04: MySQL No Root Password (CWE-521)
- **Impact:** Complete database compromise; arbitrary file write capability
- **Fix:** Set strong root password; bind to localhost only

---

## 🟠 Medium-Severity Findings

### F-05: phpinfo.php Information Disclosure (CWE-200)
- **Impact:** Exposed system metadata and configuration details
- **Fix:** Delete phpinfo.php; disable directory indexing

---

## 🛠️ Remediation Plan

| Priority | Finding | Timeline | Action |
|----------|---------|----------|--------|
| 1 | F-01 | 24 hours | Upgrade/disable vsftpd; block port 21 |
| 2 | F-06 | 24 hours | Uninstall/reinstall UnrealIRCd; block port 6667 |
| 3 | F-02 | 24 hours | Disable Telnet; enforce SSH |
| 4 | F-03 | 48 hours | Patch Samba; add firewall restrictions |
| 5 | F-04 | 48 hours | Secure MySQL; bind to localhost |
| 6 | F-05 | 7 days | Remove diagnostic files; harden web server |

---

## 📁 Repository Structure

```
InternSpark-CyberSecurity-Internship/
├── README.md                                    # This file
├── InternSpark_Internship_task1.txt            # Detailed assessment report
├── nmap_scan.txt                               # Nmap scan output
└── [Additional assessment files]
```

---

## ⚠️ Important Notes

### Disclaimer
- **This assessment was conducted in a controlled, isolated VirtualBox lab environment**
- **No external networks, public IP addresses, or third-party systems were accessed**
- **All activities are for educational and authorized testing purposes only**
- **This repository is classified as CONFIDENTIAL / INTERNAL ONLY**

### Ethical Hacking Guidelines
- ✅ Always obtain written authorization before conducting security assessments
- ✅ Use isolated test environments for practice and training
- ✅ Document all findings professionally and responsibly
- ✅ Follow responsible vulnerability disclosure practices
- ✅ Respect privacy and legal boundaries

---

## 📚 References & Resources

- **OWASP:** Open Web Application Security Project
- **NIST:** Cybersecurity Framework
- **CWE/CVE Databases:** Common Weakness & Vulnerability Enumeration
- **Metasploitable 2:** Intentionally vulnerable Linux for penetration testing practice

---

## 👤 Author Information

**Prepared By:** Rudresha RK  
**Program:** InternSpark Cybersecurity Internship  
**Date:** June 2026  
**Contact:** [Your Contact Information]

---

## 📝 License & Confidentiality

This documentation is classified as **CONFIDENTIAL / INTERNAL ONLY** and is intended solely for authorized InternSpark staff, mentors, and evaluators. Unauthorized distribution or reproduction is prohibited.

---

**Last Updated:** June 3, 2026  
**Status:** Complete - Ready for Academic Submission
