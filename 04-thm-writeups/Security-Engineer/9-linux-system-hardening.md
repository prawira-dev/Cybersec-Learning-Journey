# Linux System Hardening
## Task 1: Introduction
* **Overview:** Introduces the Linux System Hardening room, emphasizing why Linux servers are widely chosen for their reliability, robustness, and lower licensing costs compared to closed-source alternatives (like Windows Server).
* **Core Focus:** Highlights that before production deployment, Linux systems must undergo "hardening"—the process of securing systems by reducing their attack surface and mitigating security vulnerabilities.
* **Key Learning Path:** Outlines upcoming topics including physical security, filesystem encryption, firewall configurations, remote access control, service management, patch policies, and logging.

## Task 2: Physical Security
* **Overview:** Explores physical security measures, reminding administrators that a secure OS is completely vulnerable if an attacker has unrestricted physical access to the underlying hardware.
* **Key Concepts & Protections:**
    * **BIOS/UEFI Security:** Protecting system boot settings with strong passwords and disabling booting from unauthorized external media (USB or CD/DVD drives) to prevent unauthorized live-environment bypasses.
    * **GRUB Bootloader Protection:** Securing the GRUB bootloader with a password so attackers cannot modify kernel boot parameters, enter single-user mode, or reset root credentials without authentication.
    * **Console Lockout & Facilities:** Ensuring physical servers are housed in locked, temperature-controlled data centers or server rooms with strict access logs and surveillance.
* **Tools:** 
    * One tool is `grub2-mkpasswd-pbkdf2`
    * `PBKDF2` stands for **Password-Based Key Derivation Function 2**. It is a cryptographic algorithm designed to derive a secure key from a password, making it more resilient against brute-force attacks.

## Task 3: Filesystem Partitioning and Encryption
* **Overview:** Focuses on secure partition layouts and disk encryption practices to protect data at rest against physical theft or unauthorized inspection.
* **Key Concepts & Best Practices:**
    * **Dedicated Partitions:** Isolating critical directories—such as `/var`, `/var/log`, `/tmp`, and `/home`—onto separate physical partitions or logical volumes. This prevents a log-flooding or disk-filling attack from crashing the entire root file system (`/`).
    * **Filesystem Mounting Options:** Applying restrictive mount flags like `nosuid`, `noexec`, and `nodev` to shared or temporary directories to stop unauthorized script execution and privilege escalation attempts.
    * **Disk Encryption (LUKS):** Utilizing Linux Unified Key Setup (LUKS) to encrypt whole block devices, ensuring that if a hard drive is stolen or pulled from the server, the data remains completely unreadable without the decryption passphrase.

## Task 4: Firewall
* **Overview:** Explores host-based firewalls on Linux, explaining how they manage inbound and outbound network traffic, restrict unrequested connections, and prevent compromised systems from functioning arbitrarily as servers.
* **Key Concepts & Tools:**
    * **Stateful vs. Stateless:** Modern Linux firewalls track active connection states to safeguard against malformed packet bypasses.
    * **Netfilter & Front-ends:** Netfilter handles packet filtering at the Linux kernel level, managed via command-line front-ends like iptables (using chains like INPUT, OUTPUT, and FORWARD), nftables, or simpler CLI wrappers like ufw (Uncomplicated Firewall).

## Task 5: Remote Access
* **Overview:** Focuses on securing remote management interfaces (primarily OpenSSH) to prevent unauthorized remote access, credential stuffing, and brute-force attacks.
* **Key Concepts & Hardening Best Practices:**
    * **Disabling Root Login:** Configuring SSH (/etc/ssh/sshd_config) to disallow direct root logins (PermitRootLogin no), requiring administrators to log in via a standard user account before escalating privileges with sudo.
    * **Key-Based Authentication:** Replacing vulnerable password-based authentication with robust SSH public/private key pairs and disabling password logins entirely.
    * **Port and Protocol Adjustments:** Changing the default SSH port or restricting access using firewall rules and Fail2Ban.

## Task 6: Securing User Accounts
* **Overview:** Covers techniques for managing and hardening user accounts, enforcing strong credentials, and minimizing the risk of unauthorized privilege escalation.
* **Key Concepts & Best Practices:**
    * **Password Policies:** Enforcing complexity rules, expiration periods, and account lockouts after consecutive failed attempts.
    * **Privilege Management:** Ensuring the principle of least privilege by strictly auditing who has sudo access and avoiding shared administrative accounts.
    * **Account Lifecycle Management:** Regularly auditing local user accounts, removing inactive or default system accounts, and locking shells (/sbin/nologin) for service accounts that do not require interactive logins.

## Task 7: Software and Services
* **Overview:** Focuses on minimizing the software attack surface by eliminating unnecessary applications, background services, and listening daemons.
* **Key Concepts & Best Practices:**
    * **De-bloating:** Removing unused software packages and applications to minimize potential vulnerabilities and unpatched exploits.
    * **Service Management:** Disabling and stopping non-essential background services using system utilities (such as systemctl disable --now <service>) so they do not run automatically upon startup.
    * **Port Auditing:** Regularly checking listening network ports (using tools like ss -tulpn) to ensure no unauthorized or unexpected network services are active.

## Task 8: Update and Upgrade Policies
* **Overview:** Explores strategies for keeping the operating system and installed software packages patched against newly discovered security vulnerabilities.
* **Key Concepts & Best Practices:**
    * **Vulnerability Patch Management:** Establishing a routine schedule for checking, testing, and applying security updates.
    * **Automated vs. Manual Updates:** Balancing the speed of automated security patches (especially for critical zero-day vulnerabilities) with stability testing in staging environments before rolling updates out to production servers.
    * **Package Management Tools:** Leveraging native package managers (like apt or yum) to securely fetch and install signed updates from trusted repositories.

## Task 9: Audit and Log Configuration
* **Overview:** Covers centralized logging, system auditing, and monitoring configurations required for effective incident detection and forensic analysis.
* **Key Concepts & Tools:**
    * **Log Management (rsyslog / journald):** Ensuring system, authentication, and kernel logs are actively recorded, rotated properly to save disk space, and ideally forwarded to a secure remote SIEM server to prevent tampering by an attacker.
    * **Linux Auditing Framework (auditd):** Configuring auditd to monitor specific system calls, file modifications, or privilege escalations in real-time.
    * **Integrity Monitoring:** Keeping track of log file permissions and ensuring unauthorized users cannot read or clear audit trails.

## Task 10: Conclusion and Final Notes
* **Overview:** Wraps up the Linux System Hardening room with a final review of best practices.
* **Key Takeaways:**
    * System hardening is not a single one-time setup task; it is an ongoing, cyclical process of continuous auditing, patching, and configuration management.
    * Combining physical security, strict access controls, firewalls, and reliable logging builds a robust defense-in-depth architecture for any Linux environment.