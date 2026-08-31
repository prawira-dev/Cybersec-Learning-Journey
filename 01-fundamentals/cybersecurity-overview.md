# 🛡️ Cybersecurity Fundamentals: Intro & Attack/Defense Concepts

*Category: [Fundamentals](../01-fundamentals/README.md)*  
*Source: TryHackMe - Introduction to CyberSecurity*

---

## Attack (Red Team) vs Defense (Blue Team)

| Domain | Core Goal | Primary Tools & Frameworks | Key Focus |
| :--- | :--- | :--- | :--- |
| **Offensive (Red Team)** | Identify & exploit vulnerabilities before attackers do | Nmap, Burp Suite, Metasploit, MITRE ATT&CK | Exploitation, Privilege Escalation, Reconnaissance |
| **Defensive (Blue Team)** | Detect, prevent, and respond to unauthorized activity | Wireshark, SIEM (Splunk/Elastic), Snort, Firewalls | Log Analysis, Traffic Monitoring, Incident Response |

---

## CIA Triad
* **Confidentiality:** Data only accessible to authorized users (Encryption, Access Control).
* **Integrity:** Data remains untampered (Hashing, Digital Signatures).
* **Availability:** Systems remain operational and accessible (Redundancy, DDoS Protection).

> Security professionals generally evaluate incidents by asking questions like:
> * Was sensitive data exposed to unauthorized individuals?
> * Was data modified without permission?
> * Were systems or services unavailable to users when needed?

---

## Defense-in-Depth:
Implementing multiple layers of security controls (Network, Host, Application, Physical) rather than relying on a single firewall.

---

## Risk Management
* **Risk Identification:** Recognize potential threats.
* **Assessment:** Evaluate the likelihood and impact of threats/vulnerabilities
* **Mitigation:** Implement measures to reduce risk.
* **Residual Risk:** The remaining risk after mitigation.