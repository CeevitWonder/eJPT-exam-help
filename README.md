# 🎓 eJPT v2 Preparation Guide & Study Notes

> 📋 A structured, hands-on walkthrough for preparing for the **eLearnSecurity Junior Penetration Tester (eJPT) v2** certification exam.

[![eJPT](https://img.shields.io/badge/Certification-eJPT_v2-blue?logo=ine)](https://ine.com/learning/certifications/official/ejpt-junior-penetration-tester)
[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](LICENSE)
[![PDF](https://img.shields.io/badge/Download-PDF-red?logo=adobeacrobatreader)](eJPT_Study_Guide.pdf)

⚠️ **Disclaimer**: This guide contains **general study notes, command references, and methodology tips** based on publicly available information and personal learning. It does **not** include actual exam questions, answers, or proprietary content from INE/eLearnSecurity. Always review the [official eJPT exam policies](https://ine.com/pages/ejpt-exam-policies) before studying.

---

## ✨ What's Inside

| Section | Topics Covered |
|---------|---------------|
| 🔧 Pre-Exam Setup | Tool verification, wordlists, Metasploit DB, note-taking structure |
| 🚀 Reconnaissance | Host discovery, Nmap strategies, question-first methodology |
| 🔍 Service Enumeration | Web, SMB, SSH, MySQL, FTP enumeration commands |
| 💥 Exploitation | Metasploit workflows, manual exploits, reverse shells |
| 🔐 Privilege Escalation | Linux/Windows escalation checklists, credential dumping |
| 🔄 Pivoting | Autoroute, port forwarding, proxychains for internal networks |
| 📝 Exam Strategy | Time management, documentation templates, troubleshooting |

---

## 📥 Download

📄 **[eJPT.pdf](eJPT_Study_Guide.pdf)** *(Direct PDF Download)*

> 💡 Tip: Right-click → "Save link as..." to download. View online via GitHub's PDF preview.

---

## 🚀 Quick Start: Study Workflow

```
# 1. Clone this repo
git clone https://github.com/YOUR_USERNAME/ejpt-study-guide.git
cd ejpt-study-guide

# 2. Set up your lab (Kali recommended)
sudo apt update && sudo apt install -y nmap gobuster sqlmap john hashcat

# 3. Prepare wordlists
gunzip /usr/share/wordlists/rockyou.txt.gz 2>/dev/null

# 4. Follow the guide phases:
#    Phase 1: Recon (30 min) → Phase 2: Enum (3 hrs) → Phase 3: Exploit (5 hrs)
```

## 🎯 Key Study Strategies (From the Guide)
## ✅ Read All Questions First
Questions often contain hints about services, flags, or exploitation paths. Save hours by scanning all 35 questions before starting.

## ✅ Document Everything Immediately
| IP | Hostname | Services | Credentials | Flags |
|----|----------|----------|-------------|-------|
| 192.168.1.10 | WEB01 | Apache 2.4.29 | admin:admin123 | {eJPT_...} |

## ✅ Test Credential Reuse Everywhere
The same password often works across SSH, SMB, MySQL, and web logins in lab environments.

## ✅ Use Metasploit Autoroute (Not SOCKS) for Pivoting
# From Meterpreter session:
```
meterpreter> run autoroute -s 10.10.10.0/24  # Add internal subnet
meterpreter> run autoroute -p                 # Verify routes
```
## 🛠 Essential Commands Cheat Sheet
Host Discovery
```
netdiscover -r 192.168.100.0/24 -i eth0
nmap -sn 192.168.100.0/24 -oG recon/live_hosts.txt
```

## Service Enumeration
```
# Full port scan + service detection
nmap -sV -sC -p- -T4 -Pn -oN recon/[IP]_full.txt [IP]

# Web directory brute-force
gobuster dir -u http://[IP]/ -w /usr/share/wordlists/dirb/common.txt
```

## Exploitation Templates
# Metasploit workflow
```
msfconsole
search [service] [cve]
use exploit/[path]
set RHOSTS [IP]
set LHOST [your_IP]
exploit -j  # Run as job
```

## Privilege Escalation Checks
```
# Linux: SUID binaries
find / -perm -u=s -type f 2>/dev/null

# Windows: Unquoted service paths
wmic service get name,displayname,pathname,startmode | findstr /i "auto" | findstr /i /v "c:\windows" | findstr /i /v """
```

## ⚠️ Ethical Use & Certification Policies
This guide is intended for:
✅ Personal study and skill development
✅ Authorized penetration testing practice in lab environments
✅ Understanding penetration testing methodology

This guide is NOT for:
❌ Sharing actual eJPT exam questions, answers, or flags
❌ Violating INE/eLearnSecurity's Non-Disclosure Agreement
❌ Unauthorized testing of systems you do not own

## 📜 Always review the official eJPT exam policies and sign any required NDAs before attempting the certification.

## 🤝 Contributing
Found a typo? Have a better command or strategy? Contributions welcome!
Fork this repository
Create a feature branch: git checkout -b fix/typo-section-3
Make your change + commit: git commit -m "fix: correct nmap flag in enumeration"
Push and open a Pull Request

## 📚 Prefer to discuss? Open a Discussion first.
## 📄 License
This study guide is licensed under Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0).
## You are free to:
✅ Share — copy and redistribute the material
✅ Adapt — remix, transform, and build upon the material
Under these terms:
🔄 Attribution: Credit the original author
💰 NonCommercial: Do not use for commercial purposes
🔁 ShareAlike: Distribute derivatives under the same license

## 🙏 Acknowledgments
INE Academy — for the eJPT curriculum and lab platform
HackTheBox, TryHackMe — for complementary practice
The infosec community — for open-source tools and knowledge sharing
Built with ❤️ for aspiring penetration testers. Stay ethical, stay curious. 🛡️🔍
