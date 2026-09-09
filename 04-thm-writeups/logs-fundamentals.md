# Logs Fundamentals
## Intro
* **Overview:** Introduces logs as the digital footprints left behind by normal and malicious activities within a digital system, serving as essential traces for security investigations.
* **Key Use Cases of Logs:**
    * **Security Events Monitoring:** Detects anomalous behavior through real-time monitoring.
    * **Incident Investigation and Forensics:** Provides detailed information on what happened during an incident to perform root cause analysis.
    * **Troubleshooting:** Records system or application errors to help diagnose and fix issues.
    * **Performance Monitoring:** Offers insights into application performance.
    * **Auditing and Compliance:** Establishes a verifiable activity trail for auditing and regulatory compliance.
* **Learning Objectives:** Prepares learners to understand different log types, analyze them effectively, and investigate specific Windows event logs and web access logs.

## Types of Logs
* **Overview:** Explores how logs are segregated into distinct categories based on the type of information they provide, making it much easier to isolate relevant records during security troubleshooting or investigations.
* **Common Types of Logs:**
    * **System Logs:** Track operating system activities, including system startup/shutdown events, driver loading events, system errors, and hardware events.
    * **Security Logs:** Record security-related activities, such as authentication events, authorization events, security policy changes, user account changes, and abnormal activities.
    * **Application Logs:** Contain specific records regarding user interactions, application updates, changes, and errors occurring within software applications.
    * **Audit Logs:** Provide detailed trails of user actions and system changes to satisfy compliance requirements and support security monitoring.
    * **Network Logs:** Monitor incoming and outgoing network traffic, connection details, and firewall activities.
    * **Access Logs:** Track detailed access to various resources, such as web server access logs, database access logs, and API access logs.
* **Log Analysis:** The technique of extracting valuable intelligence from raw logs to detect abnormal or malicious behavior using manual or automated methods.

## Windows Event Logs Analysis
* **Overview:** Explores how Windows operating systems record operational and security activities into segregated log files (`Application`, `System`, and `Security`), which can be inspected using the built-in Event Viewer utility.
* **Key Windows Log Categories:**
    * **Application:** Records software-related errors, warnings, and compatibility issues.
    * **System:** Captures OS-level operations, driver issues, hardware events, startup/shutdown information, and service states.
    * **Security:** The most critical log for security investigations, tracking authentication attempts, user account modifications, and security policy changes.
* **Crucial Windows Event IDs:**
    * `4624`: Successful user login.
    * `4625`: Failed user login.
    * `4634`: Successful user logoff.
    * `4720`: User account created.
    * `4722`: User account enabled.
    * `4725`: User account disabled.
    * `4726`: User account deleted.
    * `4724`: Password reset attempt.
* **Investigation Workflow:** Explains how to use the Filter Current Log feature in Event Viewer to target specific Event IDs quickly during an incident investigation.

* Use this command to remote the target Windows lab machine from attacker VM
    ```bash
    xfreerdp /u:Administrator /p:logs@123 /v:<TARGET_MACHINE_IP>
    ```

## Web Server Access Logs Analysis
* **Overview:** Explores how web servers record incoming user requests and server responses into access log files (such as Apache's `access.log`), detailing the critical fields captured during web traffic.
* **Anatomy of an Apache Access Log Entry:**
    * **IP Address:** The client IP address making the request.
    * **Timestamp:** The precise date and time of the request.
    * **Request Details:** Includes the HTTP method (e.g., `GET`, `POST`), requested URL path, and HTTP version.
    * **Status Code:** The server's response indicator (e.g., `200` for success, `404` for not found, `500` for server error).
    * **User-Agent:** Detailed technical string identifying the user's operating system, browser, and device configuration.
* **Manual Log Analysis CLI Utilities:**
    * `cat`: Displays entire file contents or combines multiple log files into a single file.
    * `grep`: Searches for specific strings or patterns (such as an IP address or URL) across log lines.
    * `less`: Enables paginated, page-by-page viewing of large log files with built-in search and navigation commands (`/` to search, `n` or `N` to move through occurrences).