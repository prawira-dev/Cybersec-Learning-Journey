# OWASP Top 10 2025: Insecure Data Handling
## Intro
* **Overview:** Introduces the OWASP Top 10 2025: Insecure Data Handling room, which focuses on application behavior and user input vulnerabilities associated with how data is processed, stored, and protected.
* **Core Categories Covered:**
    * **A04: Cryptographic Failures:** Flaws in protecting sensitive data at rest or in transit due to improper encryption or weak algorithms.
    * **A05: Injection:** Vulnerabilities where untrusted user input is sent to an interpreter as part of a command or query, leading to unauthorized execution or data access.
    * **A08: Software or Data Integrity Failures:** Risks related to code and infrastructure that protect against integrity violations without verifying updates, critical data, or CI/CD pipelines.
* **Lab Environment Setup:** Emphasizes deploying the practical lab virtual machine via the TryHackMe platform to complete the hands-on exploitation challenges.

## A04: Cryptographic Failures
* **Overview:** Explores Cryptographic Failures, which occur when sensitive data is inadequately protected due to a lack of encryption, faulty implementations, missing security measures, or relying on outdated or weak algorithms (such as MD5 and DES).
* **Key Concepts & Risks:**
    * Failing to hash passwords securely or exposing encryption keys.
    * Rolling Your Own Cryptography: Creating custom, unvetted encryption algorithms instead of using well-established, industry-standard cryptographic libraries.
    * Hard-coding access credentials or secrets directly into source code, repositories, or configuration files.
* **Prevention Strategies:**
    * Choose strong, modern algorithms and implement them correctly.
    * Hash passwords using robust, slow hashing functions like bcrypt, scrypt, or Argon2.
    * Rely strictly on trusted, industry-standard libraries rather than custom implementations.
    * Store secrets and credentials securely using dedicated key management systems or environment variables.
* **Practical Challenge:** Involves exploring the note-sharing web application running on port 8001 of the lab machine to decrypt protected notes utilizing weak, shared derivative keys and retrieve the hidden flag.

## A05: Injection
* **Overview:** Explores Injection, a classic and enduring vulnerability where applications take untrusted user input and pass it directly into an interpreter or command processor (such as a database query engine, shell, or templating engine) without proper sanitization or parameterization.
* **Common Forms of Injection:**
    * **SQL Injection (SQLi):** Manipulating database queries via user-supplied parameters on login forms or inputs.
    * **Command Injection:** Passing raw input directly to the system shell to execute unauthorized OS commands.
    * **AI Prompt Injections:** Injecting instructions into AI models to bypass safety filters or alter expected execution behaviors.
    * **Server-Side Template Injection (SSTI):** Abusing an application's dynamic template rendering engine to execute arbitrary code or retrieve sensitive files.
* **Prevention Strategies:**
    * Treat all user input as untrusted.
    * Use parameterized queries and prepared statements instead of string concatenation for database operations.
    * Avoid functions that pass input directly to the system shell, relying instead on safe APIs.
    * Enforce strict input validation, data type checking, and character escaping before processing begins.
* **Practical Challenge:** Involves exploiting a Server-Side Template Injection (SSTI) vulnerability on the practical web application running on port `8000` of the lab machine to read the local `flag.txt` file.

## A08: Software or Data Integrity Failures
* **Overview:** Explores Software or Data Integrity Failures, which happen when an application blindly trusts external code, updates, or serialized data without verifying their authenticity, integrity, or origin.
* **Key Concepts & Risks:**
    * Accepting software updates, scripts, or configuration files from untrusted sources without cryptographic validation (such as checksums or digital signatures).
    * Failing to validate critical data that dictates application logic.
    * *Insecure Deserialization:* Processing serialized data (like Python `pickle` objects) from untrusted user inputs, which can allow malicious actors to achieve remote code execution.
* **Prevention Strategies:**
    * Establish strict trust boundaries by cryptographically verifying all software packages, updates, and critical artifacts before execution.
    * Avoid deserializing untrusted data whenever possible, or implement secure deserialization practices and robust integrity checks.
    * Enforce security controls throughout build processes and CI/CD pipelines.
* **Practical Challenge:** Involves generating a malicious Python pickle-serialized payload to read the contents of `flag.txt` via the web application running on port `8002` of the lab machine.