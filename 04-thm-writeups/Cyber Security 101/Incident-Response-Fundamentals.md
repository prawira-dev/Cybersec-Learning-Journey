# Incident Response Fundamentals
## Intro
* **Overview:** Introduces the fundamental concepts of Incident Response (IR), explaining how digital systems constantly generate massive volumes of routine activity and logs.
* **Events to Alerts:** When security tools analyze ingested logs and flag potential malicious behavior, they generate an alert. Security teams then triage these alerts to separate harmless noise from real threats:
    * **False Positives:** Alerts triggered by legitimate activities (e.g., a high-volume cloud data backup incorrectly flagged as exfiltration).
    * **True Positives:** Alerts that successfully identify genuine harmful activity, which are officially classified as Incidents.
* **Room Learning Objectives:** Prepares learners to explore incident categories, understand SANS and NIST response frameworks, utilize detection tools and playbooks, and practice hands-on triage workflows.

## What are Incidents?
* **Overview:** Explores how security solutions ingest routine device events and logs, and what happens when they flag potential threats.
* **Alert Classification:**
    * **False Positive:** An alert triggered by benign activity that mimics a threat (such as a large cloud data backup incorrectly flagged as suspicious data exfiltration).
    * **True Positive:** An alert that correctly identifies genuine harmful activity (such as a targeted phishing email). True positives are officially classified as Incidents.
* **Incident Severity:** Explains how security teams prioritize multiple concurrent incidents by categorizing them into severity levels—ranging from low and medium to high and critical—with critical incidents requiring immediate response.

## Types of Incidents
* **Overview:** Explores the various categories of security incidents that can impact an organization, noting that different incidents possess unique potentials for damage depending on the victim's business model.
* **Common Types of Security Incidents:**
    * **Malware Infections:** Incidents involving malicious programs (such as text, documents, or executables) designed to damage systems, networks, or applications, often triggered by downloaded email attachments or malicious links.
    * **Security Breaches:** Unauthorized access gained by threat actors to confidential data that should only be accessible to authorized personnel.
    * **Data Leaks:** Incidents where sensitive personal or organizational information is exposed to unauthorized entities, which can happen intentionally (for extortion or reputational damage) or unintentionally via human error and misconfigurations.
    * **Insider Attacks:** Malicious activities initiated intentionally by individuals within an organization (such as a disgruntled employee), which are particularly hazardous due to the insider's elevated access to internal resources.
    * **Denial of Service (DoS) Attacks:** Incidents aimed at disrupting system or application availability by flooding networks or services with false requests until legitimate resources are completely exhausted.

## Incident Response Process
* **Overview:** Explores structured approaches to incident response using industry-standard frameworks from SANS and NIST to handle diverse security incidents effectively.
* **The SANS Incident Response Framework (PICERL):**
    * **Preparation:** Building necessary resources ahead of time, such as establishing IR teams, writing incident response plans, deploying security tools, and conducting employee security awareness training (e.g., against phishing emails).
    * **Identification:** Monitoring for and detecting abnormal behavior that indicates an incident (e.g., catching abnormal data exfiltration caused by a compromised host).
    * **Containment:** Minimizing the spread and impact of an ongoing attack by isolating compromised machines or disabling compromised user accounts.
    * **Eradication:** Removing the root threat, malicious software, or vulnerabilities completely from the environment.
    * **Recovery:** Restoring affected systems from clean backups or rebuilding them, then testing them thoroughly before bringing them back online.
    * **Lessons Learned:** Conducting post-incident reviews and post-mortems to identify detection gaps and improve the organization's security posture for future events.
* **The NIST Incident Response Framework:** A streamlined 4-phase equivalent framework that aligns closely with the SANS lifecycle.
* **The Incident Response Plan:** A formal, senior-management-approved document outlining organizational procedures, roles and responsibilities, IR methodologies, communication plans with stakeholders, and escalation paths.

## Incident Response Techniques
* **Overview:** Explores the specialized security tools and documentation frameworks used to detect, analyze, and handle incidents during the identification and response phases.
* **Key Detection & Response Technologies:**
    * **SIEM (Security Information and Event Management):** Centralizes and correlates logs from multiple sources across the network to identify anomalies and incidents.
    * **AV (Antivirus):** Scans systems regularly to detect and flag known malicious programs.
    * **EDR (Endpoint Detection and Response):** Deployed on individual endpoints to protect against advanced threats, offering the capability to execute response actions like containment and eradication.
* **Playbooks vs. Runbooks:**
    * **Playbooks:** Comprehensive, high-level guidelines and structured workflows detailing step-by-step procedures to handle specific types of security incidents (such as responding to a phishing email attack).
    * **Runbooks:** Detailed, procedural execution steps for specific tasks carried out during different incidents.

## Lab Work Incident Response
* **Overview:** Provides a hands-on practical simulation where you investigate an enterprise-wide incident triggered by a targeted phishing email campaign delivering malicious attachments.
* **Investigation Scope & Steps:**
    * **Email Analysis:** Identifies the malicious sender name and the threat vector utilized in the attack.
    * **Impact Assessment:** Determines the total count of internal employee devices that downloaded the malicious email attachment versus those that actually executed the payload.
    * **Timeline Reconstruction:** Analyzes event logs across infected hosts to trace the chain of infection.
* **Completion:** Successfully carrying out the incident response steps on all affected hosts and documenting the findings reveals the final exercise flag.