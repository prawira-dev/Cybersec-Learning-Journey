# OWASP Top 10 2025: Application Design Flaws
## Intro
* Overview: Introduces the OWASP Top 10 2025: Application Design Flaws room, which shifts focus from implementation bugs to architectural and design-level weaknesses in systems.

Core Categories Covered:

AS02: Security Misconfigurations: Flaws stemming from insecure default settings, improper error handling, or exposed unnecessary features.

AS03: Software Supply Chain Failures: Risks introduced via compromised third-party components, libraries, or external dependencies.

AS04: Cryptographic Failures: Weaknesses in protecting sensitive data at rest or in transit due to improper encryption or outdated algorithms.

AS06: Insecure Design: Architectural flaws that cannot be fixed by a simple code patch because the core logic or design itself is fundamentally flawed.

Lab Environment Setup: Emphasizes deploying the practical lab virtual machine via the TryHackMe platform to complete the hands-on challenges.

## AS02: Security Misconfigurations
* **Overview:** Explores Security Misconfigurations, which occur when systems, infrastructure, or applications are deployed with unsafe defaults, incomplete settings, or exposed services rather than code-level bugs.
* **Why It Matters:** Modern technology stacks involve complex cloud environments, APIs, and containers. A single exposed administrative dashboard, unauthenticated endpoint, or open storage bucket can give attackers an immediate entry point, as famously seen in incidents like the 2017 [AWS] S3 bucket exposure by Uber.
* **Common Patterns:**
    * Default credentials or weak passwords left unchanged.
    * Unnecessary services or management interfaces exposed to the public internet.
    * Misconfigured cloud storage permissions (AWS S3, Azure Blob, GCP buckets).
    * Unrestricted API access lacking authentication or authorization.
    * Verbose error messages that reveal stack traces, framework versions, or internal architecture details.
    * Outdated software components, frameworks, or container configurations.
    * Exposed AI or machine learning endpoints without proper access controls.
    * Prevention Strategies: Harden default configurations, enforce least-privilege access across all environments, limit network exposure via proper segmentation, automate regular configuration audits, and suppress detailed stack traces from user-facing error messages.

## AS03: Software Supply Chain Failures
* **Overview:** Explores Software Supply Chain Failures, which occur when modern applications depend on external components, libraries, services, or models that are compromised, outdated, or lacking proper verification.
* **Why It Matters:** Because applications are built from numerous third-party packages, APIs, and models, a single compromised dependency can compromise an entire system without attackers ever needing to touch custom application code.
* **Common Patterns & Real-World Risks:**
    * Using unverified or unmaintained libraries and dependencies.
    * Automatically installing packages or updates without validation.
    * Over-reliance on third-party AI models without ongoing monitoring or auditing.
    * Insecure CI/CD build pipelines that allow tampering or code injection (such as historical incidents like the SolarWinds Orion compromise).
* **Protection Strategies:** Verify all third-party components prior to use, patch dependencies regularly, sign and audit software packages, lock down CI/CD pipelines, and implement runtime monitoring to detect unusual behavior from external dependencies or AI models.

## AS04: Cryptographic Failures
* **Overview:** Explores Cryptographic Failures, which occur when encryption is implemented incorrectly, or omitted entirely, allowing attackers to access sensitive private data like passwords, tokens, or personal information.
* **Common Patterns & Real-World Risks:**
    * Using deprecated or weak algorithms (such as MD5, SHA-1, or ECB mode).
    * Hard-coding secrets directly within application code or configuration files.
    * Poor key rotation or management practices.
    * Failing to encrypt sensitive data at rest or in transit.
    * Using self-signed or invalid TLS certificates.
    * Exposing unencrypted model parameters or sensitive inputs in AI/ML systems.
* **Protection Strategies:** Enforce strong modern algorithms (like AES-GCM or ChaCha20-Poly1305) and TLS 1.3, utilize secure key management services (such as Azure Key Vault, AWS KMS, or HashiCorp Vault), rotate secrets regularly, maintain a complete certificate inventory, and ensure automation agents never expose plaintext credentials.

## AS06: Insecure Design
* **Overview:** Explores Insecure Design, which focuses on architectural and logical flaws baked into a system from its inception due to skipped threat modelling, poor business logic, or flawed security assumptions.
* **Why It Matters:** Unlike implementation bugs, you cannot simply patch an insecure design because the core workflow, trust boundaries, and logic itself are fundamentally flawed (such as early Clubhouse assumptions that mobile client restrictions alone were enough to protect backend endpoints).
* **Insecure Design in the AI Era:**
    * **Prompt Injection:** When user input blends with system prompts, allowing attackers to hijack context or exfiltrate data.
    * **Blind Trust:** Building fragile systems that act on AI outputs without human oversight or validation.
    * **Poisoned Models:** Utilizing models from unverified sources or fine-tuned on unsafe data that embed hidden backdoors.
* **Prevention Strategies:** Build threat modeling into every development stage, treat all model inputs/outputs as untrusted, separate system prompts from user content, require human review for high-risk actions, enforce strict least-privilege access, and continuously monitor systems for logic flaws.
