# OWASP Top 10 2025: IAAA Failures
## Intro
* **Overview:** Introduces the OWASP Top 10 2025: IAAA Failures room on TryHackMe, which focuses on security flaws tied to the applied IAAA (Identity, Authentication, Authorisation, and Accountability) model.
* **Core Categories Covered:**
    * **A01: Broken Access Control:** Failures where users can act outside of their intended permissions.
    * **A07: Authentication Failures:** Weaknesses in confirming user identities securely.
    * **A09: Logging & Alerting Failures:** Insufficient monitoring that allows breaches to go unnoticed.
* **Target Audience:** Designed as a beginner-friendly module combining theoretical concepts with practical, hands-on challenges.

## What is IAAA?
* **Overview:** Explores the IAAA framework, which serves as a sequential model for how user identities and actions are managed and verified in applications. Each level relies on the previous one and cannot be skipped.
* **The Four Pillars of IAAA:**
    * **Identity:** The unique account identifier (such as a username or email) representing a person or service.
    * **Authentication:** The process of proving that identity using credentials like passwords, multi-factor OTPs, or passkeys.
    * **Authorisation:** Determining and enforcing what permissions or resources that verified identity is allowed to access.
    * **Accountability:** Recording, logging, and alerting on actions to track who did what, when, and from where.
* **Connection to Security Failures:** Highlights that vulnerabilities in the OWASP Top 10 (2025) often stem from breakdowns in how these components are implemented, allowing attackers to access unauthorized data or escalate privileges.

## A01: Broken Access Control
* **Overview:** Explores Broken Access Control, which occurs when applications fail to properly restrict what authenticated users can see or do, often allowing them to access resources belonging to other users or perform unauthorized administrative actions.
* **Key Concepts:**
    * **Insecure Direct Object Reference (IDOR):** A common type of access control vulnerability where an application exposes a direct reference to an internal implementation object (such as a database key or accountID parameter in a URL) without validating whether the user is authorized to view it.
    * **Horizontal Privilege Escalation:** Gaining access to data or accounts belonging to another user who holds the exact same permission level or role (e.g., viewing another customer's bank profile by changing an ID parameter).
    * **Vertical Privilege Escalation:** Gaining access to higher-level privileges and restricted administrative functionalities that normal users should never reach.
    * **Practical Context:** Demonstrates how simple manipulation of identifier parameters (like changing IDs in a URL) can bypass client-side assumptions and expose sensitive data.

## A07: Authentication Failures
* **Overview:** Focuses on Authentication Failures, which occur when an application fails to reliably verify or bind a user's identity.
* **Common Causes:**
    * **Username Enumeration:** Allowing attackers to discover valid system accounts through error messages or response timing.
    * **Weak or Guessable Passwords:** Lack of appropriate rate-limiting or lockout mechanisms.
    * **Logic Flaws:** Vulnerabilities in the registration, password reset, or login flow (such as improper case handling or unique index enforcement on usernames).
    * **Insecure Sessions:** Flaws in session management, cookie handling, or token security.
* **Practical Challenge:** Demonstrates how registration logic flaws (like registering a variant with mixed capitalization, such as aDmiN) can bypass checks against existing accounts like admin and grant unintended access to administrative dashboards.

## Task 5: A09: Logging & Alerting Failures
* **Overview:** Focuses on Logging & Alerting Failures, which happen when applications fail to properly record, monitor, or alert on security-relevant events, leaving defenders blind to active attacks.

* **The Accountability Link:** Highlights that robust logging is the foundational backbone of the Accountability pillar in IAAA, as it provides the forensic evidence required to prove who did what, when, and from where.
* **Common Failures:** Poor logging practices include missing authentication event records, vague error outputs, a lack of automated alerts for brute-force attempts or privilege changes, short log retention periods, or storing logs in insecure locations where attackers can easily tamper with them.
* **Practical Investigation:** Demonstrates how analyzing SIEM application logs allows security analysts to trace sequential attack patterns—such as spotting a brute-force login sequence against an administrative account followed immediately by unauthorized access to sensitive endpoints.

## 
