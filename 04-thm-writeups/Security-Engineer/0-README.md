# 🛠️ TryHackMe - Security Engineer Path

Documentation and walkthrough notes for the **Security Engineer** learning path on TryHackMe. This page serves as a progress tracker, module breakdown, and direct index to the writeup files.

---

## 📊 Progress Overview

- **Total Completed Topics:** 35 / 35 (100.0%)
- **Status:** 🟢 Completed (Path 100% Complete)

| Module | Module Name | Topics / Rooms | Completed | Status |
| :---: | :--- | :---: | :---: | :---: |
| **01** | Introduction to Security Engineering | 4 | 4 | 🟢 Completed |
| **02** | Threats and Risks | 4 | 4 | 🟢 Completed |
| **03** | Network and System Security | 9 | 9 | 🟢 Completed |
| **04** | Software Security | 10 | 10 | 🟢 Completed |
| **05** | Managing Incidents | 4 | 4 | 🟢 Completed |
| **06** | OWASP Top 10 (2025) | 4 | 4 | 🟢 Completed |

---

## 📚 Module Breakdown & Checklist

### Module 1: Introduction to Security Engineering
- [x] **[Security Engineer Intro](./1-intro.md)**
  - Explores the day-to-day role, expectations, and core qualifications of an enterprise security engineer.
- [x] **[Principles of Security](../Cyber%20Security%20101/security-principles.md)**
  - Introduction to foundational concepts like the CIA Triad (Confidentiality, Integrity, Availability), defence-in-depth, and least privilege.
- [x] **[Cryptography Fundamentals](./2-cryptography-intro.md)**
  - Introduction to symmetric/asymmetric encryption, hashing, key exchange, and PKI.
- [x] **[Identity and Access Management (IAM)](./3-identityandaccess-management.md)**
  - Fundamentals of authentication, authorization, SSO, and MFA models.

### Module 2: Threats and Risks
- [x] **[Threat Modeling](./5-threat-modelling.md)**
  - Frameworks (e.g., STRIDE, PASTA, DREAD) to identify, categorize, and prioritize threats to an organization.
- [x] **[Risk Assessment & Management](./6-risk-management.md)**
  - Quantitative and qualitative methods for calculating risk, asset valuation, and risk mitigation strategies.
- [x] **[Governance & Regulation](./4-governance-regulation.md)**
  - Explores information security governance, international standards (ISO 27001, NIST SP 800-53), compliance, and GRC frameworks.
- [x] **[Cyber Threat Intelligence (CTI) & Vulnerability Management](./7-vulnerability-management.md)**
  - Utilizing threat feeds, indicators of compromise (IoCs), vulnerability lifecycles, and MITRE ATT&CK mapping.

### Module 3: Network and System Security
- [x] **[Secure Network Architecture](./8-secure-network-architecture.md)**
  - Designing defense-in-depth enterprise networks, DMZs, zero trust architectures, and traffic filtering.
- [x] **[Linux System Hardening](./9-linux-system-hardening.md)** — Securing services, user permissions, kernel parameters, and baseline CIS benchmarks.
- [x] **[Microsoft Windows Hardening](./10-microsoft-windows-hardening.md)** — Group policies, attack surface reduction (ASR), and endpoint security configurations.
- [x] **[Active Directory Hardening](./11-active-directory-hardening.md)** — Protecting identity stores, tiering models, Kerberos security, and delegation controls.
- [x] **[Network Device Hardening](./12-network-device%20hardening.md)**
  - Hardening switches, routers, and firewalls; disabling insecure management interfaces and enforcing secure access.
- [x] **[Network Security Protocols](./13-network-security-protocols.md)** — Deep dive into securing network architectures, firewalls, IDS/IPS, segmentation, and secure protocols (TLS/SSH/IPsec).
- [x] **[Virtualization and Containers](./14-virtualization%20and-containers.md)**
  - Securing hypervisors, container runtimes (Docker/Kubernetes), image signing, and namespace isolation.
- [x] **[Cloud Security Foundations](./15-intro-to-acloudsecurity.md)**
  - Core security models (IaaS, PaaS, SaaS), cloud configuration management, IAM policies, and securing multi-tenant cloud environments.
- [x] **[Auditing and Monitoring](./16-auditing-and-monitoring.md)**
  - Centralized log architectures (Linux/Windows), log daemons, event correlation, and SIEM fundamentals.

### Module 4: Software Security
- [x] **[OWASP API Security Top 10 - Part 1](./17-owasp-api-security-top_10%20-%201.md)** ([TryHackMe](https://tryhackme.com/room/owaspapisecuritytop105w))
  - Broken Object Level Authorization, Broken Authentication, Broken Object Property Level Authorization, Unrestricted Resource Consumption, Broken Function Level Authorization.
- [x] **[OWASP API Security Top 10 - Part 2](./18-owasp-api-security-top_10%20-%202.md)** ([TryHackMe](https://tryhackme.com/room/owaspapisecuritytop10d0))
  - Unrestricted Access to Sensitive Business Flows, Server-Side Request Forgery (SSRF), Security Misconfiguration, Improper Inventory Management, Unsafe Consumption of APIs.
- [x] **[Secure Software Development Life Cycle (SSDLC)](./19-ssdlc.md)** ([TryHackMe](https://tryhackme.com/room/securesdlc))
  - Integrating security practices at every phase of software development (OWASP SAMM, BSIMM, NIST SSDF).
- [x] **[Static Application Security Testing (SAST)](./20-sast.md)** ([TryHackMe](https://tryhackme.com/room/sast))
  - Code-level vulnerability analysis without executing the application.
- [x] **[Dynamic Application Security Testing (DAST)](./21-dast.md)** ([TryHackMe](https://tryhackme.com/room/dastzap))
  - Testing running applications for security flaws using automated tools like OWASP ZAP.
- [x] **[Weaponizing Vulnerabilities](./22-weaponizing-vulnerabilities.md)** ([TryHackMe](https://tryhackme.com/room/weaponizingvulnerabilities))
  - Understanding how software vulnerabilities are chained and turned into functional exploits.
- [x] **[Introduction to DevSecOps](./23-Introduction-to-DevSecOps.md)** ([TryHackMe](https://tryhackme.com/room/introductiontodevsecops))
  - Embedding security automation, shift-left culture, and automated scanners into CI/CD pipelines.
- [x] **Mother's Secret** ([TryHackMe](https://tryhackme.com/room/codeanalysis))
  - Practical code review and API vulnerability analysis.
- [x] **[Traverse](./25-traverse.md)** ([TryHackMe](https://tryhackme.com/room/traverse))
  - Hands-on identification and exploitation of directory traversal, IDOR vulnerabilities, and defacement remediation.
- [x] **[NoScope: Finding RCE](./26-no-scope-finding-rce.md)** ([TryHackMe](https://tryhackme.com/room/noscoperce))
  - Analysis of remote code execution vulnerabilities in modern software stack components (Mozilla Rhino sandbox breakout).

### Module 5: Managing Incidents
- [x] **[Intro to IR and IM](./27-intro-to-ir-im.md)** ([TryHackMe](https://tryhackme.com/room/introtoirandim))
  - Core principles of Incident Response (IR) and Incident Management (IM) lifecycles, team roles, and common pitfalls.
- [x] **[Logging for Accountability](./28-logging-for-accountability.md)** ([TryHackMe](https://tryhackme.com/room/loggingforaccountability))
  - Role of centralized log collection, audit trails, SIEM ingestion, and non-repudiation in incident detection and response.
- [x] **[Becoming a First Responder](./29-becoming-a-first-responder.md)** ([TryHackMe](https://tryhackme.com/room/becomingafirstresponder))
  - Tactical procedures for evidence preservation (RFC 3227), containment methods, BCP/DRP, incident documentation, and DFIR handover.
- [x] **[Cyber Crisis Management](./30-cyber-crysis-management.md)** ([TryHackMe](https://tryhackme.com/room/cybercrisismanagement))
  - Strategic leadership during catastrophic cyber events, executive communication, and business continuity.

### Module 6: OWASP Top 10 (2025)
- [x] **[OWASP Top 10 2025: IAAA Failures](../Cyber%20Security%20101/owasp-iaaafailures.md)**
  - Identification, Authentication, Authorization, and Accountability flaws (A01, A07, A09).
- [x] **[OWASP Top 10 2025: Application Design Flaws](../Cyber%20Security%20101/owasp-Application-Design-Flaws.md)**
  - Flaws rooted in architecture and system logic (A02, A03, A06, A10).
- [x] **[OWASP Top 10 2025: Insecure Data Handling](../Cyber%20Security%20101/owasp-Insecure-Data-Handling.md)**
  - Cryptographic failures, sensitive data exposure, and data processing issues (A04, A05, A08).
- [x] **Topic Transition Recap**
  - Practical review assessment connecting application security and incident handling concepts.