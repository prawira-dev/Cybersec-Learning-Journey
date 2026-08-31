# Tools Cheatsheet - Cybersecurity

Dokumentasi lengkap dan referensi cepat untuk tools-tools yang digunakan dalam cybersecurity. Folder ini berisi cheatsheet, command reference, dan contoh penggunaan dari berbagai tools populer.

## 📋 Daftar Tools

### Network Analysis & Packet Capture
- **[tcpdump](./tcpdump.md)** - Command-line packet analyzer untuk menangkap dan menganalisis traffic jaringan
  - Capture packet dari interface spesifik
  - Filter berdasarkan protocol, port, dan IP
  - Simpan dan analisis file pcap
  - Analisis DNS, HTTP, dan protokol lainnya

### Reconnaissance & Information Gathering
- **nmap** - Network mapper untuk scanning port dan service discovery
  - Port scanning (SYN, UDP, ACK)
  - Service version detection
  - OS fingerprinting
  - Vulnerability detection

- **whois** - Domain information lookup
  - Registrar details
  - Domain ownership
  - Contact information

- **dig / nslookup** - DNS query tools
  - DNS resolution
  - MX record lookup
  - NS record enumeration

### Penetration Testing
- **metasploit** - Framework untuk penetration testing
  - Exploit modules
  - Payload generation
  - Post-exploitation modules
  - Auxiliary scanners

- **burp-suite** - Web application testing
  - Proxy interceptor
  - Scanner
  - Intruder
  - Decoder

- **sqlmap** - SQL injection testing
  - Automated SQL injection detection
  - Database enumeration
  - Data extraction

### Vulnerability Scanning
- **OpenVAS** - Open source vulnerability assessment
  - Comprehensive vulnerability scanning
  - Report generation
  - Risk assessment

- **nessus** - Professional vulnerability scanner
  - Network scanning
  - Plugin-based detection
  - Compliance checking

### Cryptography & Encoding
- **openssl** - SSL/TLS toolkit
  - Certificate generation
  - Encryption/Decryption
  - Hash functions
  - Digital signatures

- **hashcat** - Password cracking tool
  - Hash identification
  - Dictionary attacks
  - Brute force attacks

- **john-the-ripper** - Password security auditing
  - Hash cracking
  - Dictionary wordlist
  - Incremental mode

### Malware Analysis
- **wireshark** - Network protocol analyzer
  - Packet inspection
  - Traffic analysis
  - Protocol dissection

- **IDA Pro** - Reverse engineering tool
  - Binary analysis
  - Disassembly
  - Debugging

- **Ghidra** - Open source reverse engineering tool
  - Decompilation
  - Binary analysis
  - Collaborative environment

### Wireless Security
- **aircrack-ng** - Wireless security suite
  - WEP/WPA cracking
  - Packet capture
  - SSID broadcasting

- **kismet** - Wireless network detector
  - Network mapping
  - Device tracking
  - Packet logging

### Post-Exploitation
- **mimikatz** - Windows post-exploitation tool
  - Credential dumping
  - Token manipulation
  - Pass-the-hash attacks

- **enum4linux** - Linux/Samba enumeration
  - User enumeration
  - Share discovery
  - Group policy extraction

- **powershell-empire** - Post-exploitation framework
  - Agent-based
  - Modular architecture
  - Command execution

### Forensics & Incident Response
- **volatility** - Memory forensics
  - Memory dump analysis
  - Process extraction
  - Rootkit detection

- **autopsy** - Digital forensics platform
  - File system analysis
  - Timeline generation
  - Reporting

### Web Application Tools
- **OWASP ZAP** - Web application security scanner
  - Automated scanning
  - Manual testing tools
  - API testing

- **Postman** - API development & testing
  - Request builder
  - Automation
  - Mock servers

### Linux Privilege Escalation
- **LinEnum** - Local enumeration script
  - System information
  - Misconfiguration detection
  - Privilege escalation paths

- **GTFOBins** - Binary exploitation database
  - Privilege escalation vectors
  - Command execution methods

### Social Engineering
- **phishing-frenzy** - Phishing simulation
  - Email templates
  - Landing page creation
  - Statistics tracking

- **set (social-engineer toolkit)** - Social engineering framework
  - Phishing attacks
  - Payload delivery
  - Attack vectors

---

## 🚀 Quick Reference

### Common Commands

#### Network Reconnaissance
```bash
# DNS lookup
nslookup target.com
dig target.com

# WHOIS information
whois target.com

# Port scanning
nmap -sV target.com

# Packet capture
tcpdump -i eth0 -w capture.pcap
```

#### Web Scanning
```bash
# OWASP ZAP
zaproxy.sh -cmd -quickurl http://target.com

# SQLMap
sqlmap -u "http://target.com/page.php?id=1" --dbs
```

#### Exploitation
```bash
# Metasploit
msfconsole
use exploit/windows/smb/ms17_010_eternalblue

# Burp Suite
burpsuite
```

---

## 📚 Referensi Lengkap

Setiap tools memiliki file dokumentasi terperinci dengan:
- Instalasi dan konfigurasi
- Syntax dan parameter
- Use cases praktis
- Contoh command
- Best practices
- Troubleshooting

## 📖 Belajar Lebih Lanjut

- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [HackTricks](https://book.hacktricks.xyz/)
- [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)
- [GTFOBins](https://gtfobins.github.io/)
- [PentestMonkey](http://pentestmonkey.net/)

---

## ⚖️ Disclaimer

Tools-tools ini hanya boleh digunakan untuk tujuan:
- Penetration testing dengan izin tertulis
- Security research
- Educational purposes
- Defense dan incident response

Penggunaan tools ini untuk tujuan ilegal atau tanpa izin adalah **ILLEGAL**. Pengguna bertanggung jawab penuh atas penggunaan tools ini.

---

## 🔗 Kontribusi

Jika ingin menambahkan tools baru atau memperbaiki dokumentasi, silahkan buat pull request dengan:
- Dokumentasi lengkap
- Contoh penggunaan
- Use cases

---

*Last Updated: 2026-08-31*

