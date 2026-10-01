# Penetration Testing & Risk Assessment Report
**Target Environment:** Mediroza Hospital Patient Portal (Authorized Lab)  
**Author:** Muhammed Ibrahim Muhammed Hussain  
**Program:** Network Walks Cybersecurity Internship Capstone Project  
**Date:** October 2026  

---

> **⚠️ EDUCATIONAL & RESEARCH DISCLAIMER**  
> The information and documentation contained in this repository are for **educational, academic, and defensive security purposes only**. All testing was conducted in an **authorized, isolated laboratory environment** as part of an official internship capstone project. No production systems or real-world networks were accessed, scanned, or modified.

---

## 📌 Executive Summary

An authorized penetration testing engagement was conducted against the Mediroza Hospital web application to evaluate its security posture, identify potential vulnerabilities, and assess the risk of unauthorized access to sensitive patient and corporate data.

The assessment revealed critical vulnerabilities across the application's access control, data handling, and configuration management mechanisms. Most notably:
* **Authentication Bypass via SQL Injection:** Allowed administrative access to the patient portal without valid credentials.
* **Cryptographic Hash Recovery:** Weak document passphrases on PDF reports were easily recovered via dictionary attacks.
* **Metadata Information Disclosure:** ExifTool analysis revealed sensitive backend paths leading to unauthenticated SQL database backup downloads containing mock organizational data.

---

## 🛠️ Scope & Methodology

### **Target Scope**
* **Application:** Mediroza Hospital Web Application & Patient Portal  
* **Environment:** Authorised Educational Internship Lab  

### **Tools & Utilities Utilized**
* **Reconnaissance & Footprinting:** `nslookup`, `whois`, `whatweb`, `curl`, `wafw00f`, `nmap`
* **Access Control & Web Audit:** Web Browser (`Firefox`), `curl`
* **Metadata & Document Analysis:** `exiftool`, `qpdf`
* **Cryptographic Analysis:** Networkwalks Hash Calculator, Networkwalks Password Cracker

### **Testing Methodology**
The methodology was structured according to standard **OWASP Web Application Security Assessment** guidelines:
1. **Reconnaissance & Footprinting:** Identifying server headers, WAF presence, and active host ports.
2. **Authentication & Access Control Testing:** Auditing login interfaces for input validation weaknesses and authentication bypasses.
3. **Data Protection & Cryptography Review:** Testing file encryption, password strength, and data extraction risks.
4. **Information Disclosure Analysis:** Inspecting metadata properties and exposed administrative server directories.

---

## 📊 Summary of Identified Risks

| Vulnerability | Severity | CVSS v3.1 | Primary Impact |
| :--- | :---: | :---: | :--- |
| **SQL Injection (Auth Bypass)** | **Critical** | `9.8` | Complete takeover of administrative portal and access to patient records. |
| **Exposed Database Backup File** | **Critical** | `9.1` | Direct unauthenticated access to system database backups and financial records. |
| **Weak PDF Encryption Passwords** | **High** | `7.5` | Rapid offline recovery of protected patient files due to predictable passphrases. |
| **Information Leakage via Metadata** | **Medium** | `5.3` | Unintentional exposure of internal directory paths in published document properties. |

---

## 🛡️ Key Recommendations & Remediation Strategies

1. **Fix SQL Injection Vulnerabilities (Critical):**
   * Enforce **Parameterized Queries / Prepared Statements** (e.g., PDO in PHP) across all database authentication functions. Never concatenate raw user input into SQL queries.
   * Implement strict whitelist input validation on all user login forms.

2. **Secure Database Backups & Restrict File Access (Critical):**
   * Remove database backups and `.sql` dumps from the publicly accessible web server directory (`/var/www/html/`).
   * Configure web server configuration rules to block public GET requests for `.sql`, `.bak`, and `.log` file extensions.

3. **Enforce Strong Cryptographic Policies (High):**
   * Upgrade document passphrase standards to minimum 12+ character complex strings.
   * Require Multi-Factor Authentication (MFA) for all administrative and portal user logins.

4. **Implement Automated Metadata Scrubbing (Medium):**
   * Build automated Data Loss Prevention (DLP) pipelines to strip EXIF and document comments prior to rendering downloadable files.

---

## 📁 Repository Contents

* `Mediroza_Hospital_Penetration_Testing_Lab_Report.pdf` - Complete, formatted capstone project report including step-by-step proofs of concept, terminal execution logs, and vulnerability mitigation guides.

[Mediroza_Hospital_Penetration_Testing_Lab_Report.pdf](https://github.com/user-attachments/files/32935427/Mediroza_Hospital_Penetration_Testing_Lab_Report.pdf)

---

## 📜 License & Compliance

This repository is published in full compliance with GitHub's Acceptable Use Policies concerning security research and technical writing documentation.
