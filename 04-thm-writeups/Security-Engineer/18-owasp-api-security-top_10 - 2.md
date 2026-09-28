# OWASP API Security Top 10 - 2
## Task 1: Quick Recap
* **Overview:** Introduces the second part of the OWASP API Security series, setting up the lab environment to explore the remaining top API security vulnerabilities.
* **Key Learning Objectives:**
    * Identifying API security misconfigurations and improper asset management.
    * Preventing injection attacks and Denial of Service (DoS) conditions.
    * Understanding the necessity of sufficient logging and monitoring in API environments.

## Task 2: Vulnerability VI - Mass Assignment
* **Overview:** Focuses on Mass Assignment vulnerabilities, which occur when client-provided data (e.g., JSON or form payloads) is automatically bound or assigned to internal object properties without proper filtering or field allowlisting.
* **Key Concepts & Risks:**
    * **Privilege Escalation:** An attacker alters sensitive fields—such as changing `"is_admin": false` to `"is_admin": true` or updating account balances during a single update API call.
    * **Mitigation:** Avoid using broad auto-binding frameworks without explicit schema validation. Maintain a strict allowlist of editable properties per endpoint or role (e.g., using Data Transfer Objects / DTOs).

## Task 3: Vulnerability VII - Security Misconfiguration
* **Overview:** Covers common configuration errors and oversights across API servers, network channels, and backend frameworks that expose endpoints to security risks.
* **Key Risk Factors:**
    * **Verbose Error Messages:** Leaking stack traces, internal paths, or framework version details to end-users via API error responses.
    * **Unnecessary Features Enabled:** Leaving unused HTTP methods (e.g., `TRACE`, `DELETE`), default credentials, or development endpoints active in production.
    * **CORS & Transport Security:** Insecure Cross-Origin Resource Sharing (CORS) policies (like wildcards `*`) and failing to enforce HTTPS/TLS across all API routes.
* **Mitigation:** Automate hardening via security baselines, disable development features in production, and enforce centralized error handling that strips internal debug logs.

## Task 4: Vulnerability VIII - Injection
* **Overview:** Explores injection vulnerabilities in APIs, which occur when untrusted data is sent to an interpreter as part of a command or query without proper sanitization or parameterization.
* **Key Concepts & Risks:**
    * **Common Injection Vectors:** SQL Injection (SQLi), NoSQL Injection, Command Injection, and Object-Relational Mapping (ORM) injection.
    * **Impact:** Attackers can bypass authentication, extract sensitive database records, modify backend data, or execute arbitrary commands on the API server.
    * **Mitigation:** Use parameterized queries, prepared statements, built-in ORM sanitization, and strict input validation schemas to separate user data from execution logic.

## Task 5: Vulnerability IX - Improper Assets Management
* **Overview:** Covers security risks arising from maintaining outdated API versions, exposed staging/debug endpoints, or undocumented API interfaces ("Shadow APIs").
* **Key Concepts & Risks:**
    * **Version Controls:** Leaving legacy API endpoints (e.g., `/v1/user`) active when security patches were only applied to newer versions (e.g., `/v2/user`).
    * **Environment Isolation:** Exposing non-production environments (like staging, testing, or sandbox APIs) to the public internet without proper access controls.
* **Mitigation:** Maintain up-to-date API documentation (e.g., OpenAPI/Swagger), implement automated asset discovery, and enforce strict deprecation and retirement policies for legacy endpoints.

## Task 6: Vulnerability X - Insufficient Logging & Monitoring
* **Overview:** Focuses on the failures in logging API activities and monitoring suspicious behaviors, which allows attackers to conduct reconnaissance and persistent attacks undetected.
* **Key Concepts & Risks:**
    * **Lack of Visibility:** Failing to log failed authentication attempts, access control violations, or input validation errors across API endpoints.
    * **Incident Delay:** Without real-time alerting and log centralization, malicious activities can go unnoticed for extended periods.
* **Mitigation:** Centralize API access logs into a SIEM, enforce audit logging for all critical transactions, set up automated alerting thresholds for abnormal traffic spikes, and ensure log integrity against tampering.

## Task 7: Conclusion
* **Overview:** Concludes the OWASP API Security Top 10 - 2 room by reviewing the full spectrum of API risks.
* **Key Takeaway:** Securing APIs requires a continuous, multi-faceted approach—combining strict input validation, proper asset management, secure backend configurations, and robust real-time auditing across all API endpoints.