# 🛡️ DevSecOps Learning Path - TryHackMe

## 📌 Curriculum Overview

The learning path is structured into 5 core modules:
DevSecOps
├── 1. Secure Software Development
├── 2. Security of the Pipeline
│   ├── Intro to Pipeline Automation
│   ├── Source Code Security
│   └── CI/CD and Build Security
├── 3. Security in the Pipeline
├── 4. Container Security
└── 5. Infrastructure as Code

---

## 📚 Module & Room Breakdown

### 1. Secure Software Development
Covers the foundational concepts of DevSecOps, comparing DevOps vs. DevSecOps, and integrating security gates directly into the SDLC.
* **Key Topics:** SDLC models, Threat Modeling, Security Gates, and Shift-Left practices.

---

### 2. Security of the Pipeline
Focuses on platform security, build tools, and protecting source code as it travels through development, testing, and deployment.

* **[Intro to Pipeline Automation](https://tryhackme.com/room/introtopipelineautomation)**
  * Fundamentals of DevOps automation.
  * Identifying common security risks in automated workflows.
* **[Source Code Security](https://tryhackme.com/room/sourcecodesecurity)**
  * Version Control Systems (VCS) & Git mechanics.
  * Credential hygiene, detecting hardcoded secrets (API keys, passwords, private keys), and using secret scanners (Gitleaks, TruffleHog).
* **[CI/CD and Build Security](https://tryhackme.com/room/cicdandbuildsecurity)**
  * Securing build platforms (GitLab CI, Jenkins) and runners.
  * Access control, credential management, and mitigating Poison Pipeline Execution (PPE) attacks.

---

### 3. Security in the Pipeline
Focuses on automated security testing embedded directly within the pipeline.

* **Key Topics:**
  * **SAST (Static Application Security Testing):** Code analysis for vulnerabilities before compilation.
  * **DAST (Dynamic Application Security Testing):** Testing running applications for runtime vulnerabilities.
  * **SCA (Software Composition Analysis):** Managing third-party dependencies and supply chain security.

---

### 4. Container Security
Covers containerization security from image building to runtime protection.

* **Key Topics:**
  * Docker security best practices and privilege management.
  * Container image vulnerability scanning.
  * Runtime protection and isolating container environments.

---

### 5. Infrastructure as Code (IaC)
Focuses on defining and securing cloud infrastructure using code.

* **Key Topics:**
  * IaC tools (Terraform, Ansible, CloudFormation).
  * Automated misconfiguration scanning before deployment.
  * Enforcing least-privilege policies in cloud environments.

---

## 🛠️ Tools & Technologies Covered

| Category | Tools / Technologies |
| :--- | :--- |
| **Version Control** | Git, GitHub, GitLab |
| **CI/CD Automation** | Jenkins, GitLab CI |
| **Secret Scanning** | Gitleaks, TruffleHog |
| **Containers & IaC** | Docker, Terraform |
| **Security Testing** | SAST, DAST, SCA tools |

---

## 🎯 Progress Tracker

- [x] Module 1: Secure Software Development
- [ ] Module 2: Security of the Pipeline *(In Progress)*
- [ ] Module 3: Security in the Pipeline
- [ ] Module 4: Container Security
- [ ] Module 5: Infrastructure as Code