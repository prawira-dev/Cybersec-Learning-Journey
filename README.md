# Cybersec-Learning-Journey: Infrastructure & Security Knowledge Base

Welcome to my technical documentation and learning journal repository. This repository serves as my personal knowledge base and a public portfolio showcasing my career transition from an **Air Traffic Safety Electronics Personnel (ATSEP)** at AirNav Indonesia to a **Cybersecurity Specialist**.

---

## 👤 About Me
* **Background:** Telecommunications & Critical Infrastructure Technician a.k.a ATSEP Technician at AirNav Indonesia.
* **Core Focus:** OT/ICS Security, Network Security, Incident Response, & Penetration Testing.
* **Primary Platforms:** TryHackMe | Hack The Box | Hands-on Home Lab.

---

## 📂 Navigation & Cheat Sheets

| Folder | Coverage / Topics | Status |
| :--- | :--- | :---: |
| **[📁 01-Fundamentals](./01-fundamentals/)** | Linux Admin, Windows OS, Networking (TCP/IP, OSI Model) | 🟢 Active |
| **[📁 02-Tools-Cheatsheet](./02-tools-cheatsheet/)** | Nmap, Wireshark, Burp Suite, Metasploit, Bash Scripting | 🟢 Active |
| **[📁 03-Concepts](./03-concepts/)** | Web Security, SOC & Incident Response, OT/ICS Security | 🔴 Inactive |
| **[📁 04-THM-Writeups](./04-thm-writeups/)** | TryHackMe Room Walkthroughs & Learning Notes | 🟢 Active |

---

## 🎯 Progress & Milestones

- [x] **PreSec Path** - TryHackMe *(Completed: Aug 2026)*
- [ ] **Cyber Security 101 Path** - TryHackMe *(In Progress)*
- [ ] **Junior Penetration Tester / SOC Level 1** - TryHackMe
- [ ] **CompTIA Security+** / **eJPT Certification**

---

## ⚡ Quick Cheat Sheet Showcase

### 1. Nmap Network Discovery
```bash
# Full scan with service version detection and default scripts on all ports
nmap -sV -sC -p- <TARGET_IP> -oN nmap_full_scan.txt
