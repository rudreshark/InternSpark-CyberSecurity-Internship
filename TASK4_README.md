# InternSpark Cybersecurity Internship - Task 4: Incident Response & Log Analysis

## 📋 Project Overview

This repository contains a comprehensive cybersecurity incident response assessment conducted as part of the **InternSpark Internship Program**. Task 4 focuses on simulating a realistic cybersecurity incident, analyzing suspicious log activity, identifying indicators of compromise, and documenting professional incident response and containment procedures.

### Project Details
- **Prepared By:** Rudresha RK
- **Institution:** InternSpark Internship
- **Task:** Task 4 - Incident Response & Log Analysis
- **Date:** June 2026
- **Classification:** CONFIDENTIAL / INTERNAL ONLY

---

## 🎯 Task 4 Objectives

✅ Simulate a realistic cybersecurity incident scenario  
✅ Analyze Windows Event Logs and SIEM sample logs for suspicious activity  
✅ Identify and document Indicators of Compromise (IOCs)  
✅ Detect anomalous patterns, failed login attempts, privilege escalation  
✅ Perform threat analysis and attribution  
✅ Document comprehensive incident response procedures  
✅ Develop containment and remediation strategies  
✅ Generate professional incident response report  

---

## 📊 Assessment Details

| Category | Details |
|----------|---------|
| **Incident Type** | Simulated Security Incident |
| **Log Sources** | Windows Event Logs, SIEM Sample Logs |
| **Analysis Environment** | Isolated lab environment |
| **Tools Used** | Windows Event Viewer, LogParser, SIEM Tools |
| **Assessment Type** | Incident Response & Forensic Analysis |
| **Incident Timeline** | [To be documented] |
| **Systems Affected** | [To be documented] |

---

## 🔧 Tools & Methodologies

### Primary Analysis Tools

| Tool | Purpose | Function |
|------|---------|----------|
| **Windows Event Viewer** | Native Windows log analysis | System, Security, Application logs |
| **LogParser** | Command-line log querying | Parse and search through logs |
| **SIEM (Splunk/ELK)** | Centralized log management | Aggregate and correlate logs |
| **Wireshark** | Network traffic analysis | Detect network-based IOCs |

---

## 🔍 Critical Windows Event IDs

### Authentication & Access
```
Event ID 4624 - Successful logon
Event ID 4625 - Failed logon attempt
Event ID 4720 - User account created
Event ID 4769 - Kerberos service ticket requested
```

### Privilege Escalation
```
Event ID 4672 - Special privileges assigned
Event ID 4673 - Privileged service called
Event ID 4674 - Operation on privileged object
```

### Process & Execution
```
Event ID 4688 - Process created
Event ID 4698 - Scheduled task created
Event ID 4700 - Scheduled task disabled
```

---

## 🚨 Indicators of Compromise (IOCs)

### File-Based IOCs
- Suspicious file extensions (.exe, .bat, .ps1, .scr, .vbs)
- Double extensions (.pdf.exe, .txt.scr)
- Files in suspicious locations (Windows\Temp, %AppData%)
- Recently created files during incident window

### Network-Based IOCs
- Connections to known malicious IPs
- DNS queries to C2 domains
- Unusual outbound traffic on non-standard ports
- Large data exfiltration volumes

### Behavioral IOCs
- Failed logon attempts (brute force)
- Privilege escalation attempts
- Process spawning from unusual locations
- Scheduled task creation
- Registry persistence mechanisms

### Account-Based IOCs
- New admin account creation
- Disabled antivirus/firewall
- Service account abuse
- Unusual login times
- Failed auth followed by success

---

## 📋 Incident Response Phases

### Phase 1: Detection & Analysis
```
1. Confirm alert authenticity
2. Check for false positives
3. Assess initial severity
4. Collect system information
5. Preserve evidence
```

### Phase 2: Containment
```
Short-Term:
1. Isolate affected systems
2. Block malicious IPs
3. Disable compromised accounts
4. Revoke credentials
5. Block malware domains

Long-Term:
1. Patch vulnerabilities
2. Update firewall rules
3. Reset passwords
4. Remove backdoors
5. Rebuild systems
```

### Phase 3: Eradication
```
1. Run antivirus scans
2. Remove malicious files
3. Clean registry entries
4. Delete scheduled tasks
5. Remove unauthorized accounts
```

### Phase 4: Recovery
```
1. Restore from clean backups
2. Patch all systems
3. Update security controls
4. Enable logging/monitoring
5. Verify functionality
```

---

## 📊 Incident Report Template

### 1. Executive Summary
```
Incident Title: [Description]
Detection Date: [Date/Time]
Severity Level: [CRITICAL/HIGH/MEDIUM/LOW]
Systems Affected: [List]
Users Impacted: [Count]
Status: [Ongoing/Contained/Resolved]
```

### 2. Incident Timeline

| Timestamp | Event | Evidence |
|-----------|-------|----------|
| YYYY-MM-DD HH:MM | [Event] | [Log ID] |
| YYYY-MM-DD HH:MM | [Event] | [Log ID] |

### 3. Threat Analysis

**Initial Access**
```
Method: [Phishing/Exploit/RDP/Other]
Entry Point: [System/User]
Date/Time: [When]
```

**Lateral Movement**
```
From: [Starting system]
To: [Target systems]
Method: [SMB/RDP/Kerberos/Other]
```

**Privilege Escalation**
```
Method: [UAC bypass/Exploit/Token impersonation]
Accounts Used: [List]
Timeline: [When]
```

### 4. Indicators of Compromise

**File Hashes**
```
MD5: [Hash]
SHA256: [Hash]
File Path: [Location]
Detection: [Date/Time]
```

**Network Indicators**
```
Source IP: [IP]
Destination IP: [IP]
Port: [Number]
Protocol: [TCP/UDP]
```

**User Accounts**
```
Username: [Account]
Status: [Active/Disabled]
Suspicious Actions: [List]
```

### 5. Detected Anomalies

**System Anomalies**
```
- [Anomaly 1]
- [Anomaly 2]
- [Anomaly 3]
Evidence: [Event IDs]
```

**Network Anomalies**
```
- [Anomaly 1]
- [Anomaly 2]
Connections: [Details]
```

**User Behavior**
```
- [Unusual access pattern]
- [Off-hour activity]
Evidence: [Event IDs]
```

### 6. Containment Actions

**Immediate Actions**
```
1. [Action] - Timestamp - Result
2. [Action] - Timestamp - Result
3. [Action] - Timestamp - Result
```

**Systems Isolated**
```
- [System name] - Reason: [Why]
- [System name] - Reason: [Why]
```

**Accounts Disabled**
```
- [Username] - Reason: [Why]
```

### 7. Remediation Steps

**Short-Term (0-24 hours)**
```
1. [Action]
2. [Action]
3. [Action]
```

**Medium-Term (1-7 days)**
```
1. [Action]
2. [Action]
```

**Long-Term (1-30 days)**
```
1. [Action]
2. [Action]
```

### 8. Recommendations

**Preventive Measures**
```
1. [Recommendation]
2. [Recommendation]
3. [Recommendation]
```

**Detection Improvements**
```
1. [Alert/Monitoring enhancement]
2. [Process improvement]
```

---

## 📁 Repository Structure

```
InternSpark-CyberSecurity-Internship/
├── TASK4_README.md                    # This file
├── incident_data/
│   ├── windows_event_logs.csv
│   ├── siem_sample_logs.csv
│   ├── firewall_logs.txt
│   └── system_logs.txt
├── analysis/
│   ├── ioc_indicators.txt
│   ├── anomalies_detected.txt
│   ├── threat_analysis.txt
│   └── timeline_reconstruction.txt
├── screenshots/
│   ├── event_viewer_1.png
│   ├── event_viewer_2.png
│   ├── siem_dashboard.png
│   ├── suspicious_events.png
│   └── privilege_escalation.png
├── reports/
│   ├── incident_response_report.md
│   ├── incident_response_report.pdf
│   ├── ioc_indicators_list.csv
│   ├── anomalies_list.csv
│   └── containment_actions.txt
└── remediation/
    ├── remediation_plan.md
    ├── patch_list.txt
    ├── firewall_rules.txt
    └── monitoring_recommendations.txt
```

---

## 🔬 Analysis Workflow

### Step 1: Collect Logs
```bash
# Export Windows Event Logs
wevtutil qe Security /format:csv > windows_security.csv
wevtutil qe System /format:csv > windows_system.csv

# Export SIEM logs
splunk search "index=main" | export csv > siem_logs.csv
```

### Step 2: Parse & Filter
```bash
# Failed logon attempts
LogParser "SELECT * FROM logs WHERE EventID=4625"

# Privilege escalation
LogParser "SELECT * FROM logs WHERE EventID=4672"

# Process creation
LogParser "SELECT * FROM logs WHERE EventID=4688"
```

### Step 3: Identify IOCs
```bash
# Extract suspicious IPs
grep -oE "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" logs.txt

# Find created files
grep "CREATE" logs.txt | grep -E "\.(exe|bat|ps1)"

# Network connections
netstat -anbp | grep ESTABLISHED
```

### Step 4: Correlate & Timeline
```
1. Timeline all events
2. Identify sequences
3. Link related events
4. Find root cause
5. Map attacker activities
```

### Step 5: Generate Report
```
1. Document findings
2. Create IOC list
3. List anomalies
4. Propose remediation
5. Finalize report
```

---

## 🛡️ Common Attack Patterns

### Credential Compromise
```
Pattern: Failed logons → Success → Privilege escalation → Process creation
Response: Disable account, reset password, revoke tokens, monitor
```

### Lateral Movement
```
Pattern: Network enumeration → Credential theft → Remote logon → Tool execution
Response: Block network paths, isolate systems, kill processes
```

### Privilege Escalation
```
Pattern: Non-admin process → Exploit → Admin token → SYSTEM process
Response: Patch vulnerability, remove rights, monitor processes
```

### Data Exfiltration
```
Pattern: File access → Large transfer → Unusual destination → Off-hours
Response: Block destination, isolate system, disable account
```

---

## 📚 References

### Incident Response Frameworks
- **NIST IR Guide:** https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-61r2.pdf
- **SANS IR:** https://www.sans.org/white-papers/
- **Microsoft IR:** https://docs.microsoft.com/en-us/windows/security/

### IOC Resources
- **VirusTotal:** https://www.virustotal.com/
- **Abuse.ch:** https://abuse.ch/
- **MITRE ATT&CK:** https://attack.mitre.org/

---

## ⚠️ Important Notes

### Best Practices
- ✅ Document every action taken
- ✅ Preserve evidence and chain of custody
- ✅ Communicate with stakeholders
- ✅ Follow incident response procedures
- ✅ Maintain confidentiality

### Legal & Compliance
- ⚠️ Comply with incident notification laws
- ⚠️ Preserve evidence for legal proceedings
- ⚠️ Follow GDPR/CCPA data protection
- ⚠️ Report to authorities if required

---

## 👤 Author Information

**Prepared By:** Rudresha RK  
**Program:** InternSpark Cybersecurity Internship  
**Date:** June 2026  
**Task:** Task 4 - Incident Response & Log Analysis

---

**Last Updated:** June 2026  
**Status:** Ready for Submission

