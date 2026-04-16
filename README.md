# 🔒 ModSecurity Hardening Rules for WordPress on CyberPanel

**Author:** Karanbir Singh | [DigmLabs.com](https://www.digmlabs.com/)
**Version:** 1.0

---

## 🚀 Overview

This repository provides a **production-ready ModSecurity ruleset** specifically designed to harden **WordPress websites hosted on CyberPanel (OpenLiteSpeed)**.

These rules are built based on real-world attack patterns observed on live servers and aim to block:

* File upload exploits
* Web shell injections
* Directory traversal attacks
* Bot scanners and automated exploitation tools
* Known CMS and framework attack vectors (e.g., ThinkPHP probes)

---

## 🛡️ What This Protects Against

### 🔴 File-Based Attacks

* Malicious PHP uploads (`.php`, `.phtml`, `.phar`)
* Execution of PHP files inside `/wp-content/uploads/`

### 🔴 Injection & Exploits

* Web shell payloads (`base64_decode`, `eval`, `gzinflate`, etc.)
* Directory traversal attempts (`../` attacks)

### 🔴 Sensitive File Access

* `.env`, `.git`, `.htaccess`, `.htpasswd`
* Direct access to `wp-config.php`

### 🔴 WordPress-Specific Hardening

* Blocks direct PHP execution in `/wp-includes/`
* Restricts POST requests to uploads directory
* Optional XML-RPC blocking

### 🔴 Bot & Scanner Protection

* Blocks common tools:

  * sqlmap
  * nikto
  * curl / wget abuse
  * python-based scanners
  * libredtail-http bots

### 🔴 Known Exploit Patterns

* ThinkPHP RCE attempts
* Generic CMS probing attacks

---

## ⚙️ Requirements

* CyberPanel (OpenLiteSpeed)
* ModSecurity enabled
* OWASP CRS installed (recommended)

---

## 📦 Installation

1. Navigate to:

   ```
   /usr/local/lsws/conf/modsec/rules.conf
   ```

2. Paste the rules from this repository

3. Restart LiteSpeed:

   ```
   systemctl restart lsws
   ```

---

## 🧪 Testing

Example test:

```
curl "https://yourdomain.com/?file=../../wp-config.php"
```

Expected result:

```
403 Forbidden
```

---

## ⚠️ Notes

* Some rules (like XML-RPC blocking) may affect plugins such as Jetpack
* Always test after applying in production environments
* Logging behavior in OpenLiteSpeed may differ from Apache/Nginx setups

---

## 🔥 Why This Exists

CyberPanel’s default ModSecurity setup often:

* Loads OWASP rules but doesn’t enforce aggressively
* Lacks WordPress-specific protections
* Leaves gaps for file upload and backdoor attacks

This ruleset closes those gaps.

---

## 🤝 Contributing

Feel free to submit pull requests or suggest improvements based on new attack patterns.

---

## 🌐 About DigmLabs

DigmLabs specializes in:

* Server security & hardening
* WordPress optimization
* Malware cleanup & prevention
* Infrastructure automation

👉 [https://www.digmlabs.com](https://www.digmlabs.com/)

---

## 📜 License

MIT License
