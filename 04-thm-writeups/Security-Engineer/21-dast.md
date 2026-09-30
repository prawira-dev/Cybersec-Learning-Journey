# DAST
## Task 1: Introduction
* **Overview:** Introduces Dynamic Application Security Testing (DAST) as a black-box security testing methodology performed by analyzing and interacting with a running application instance from an external perspective.
* **Key Learning Objectives:**
    * Understand how DAST identifies vulnerabilities in live environments.
    * Evaluate the advantages and tradeoffs of DAST compared to static analysis (SAST).
    * Learn hands-on application scanning using popular DAST tools such as OWASP ZAP.

## Task 2: Dynamic Application Security Testing (DAST)
* **Overview:** Explores the fundamental principles, mechanisms, and practical benefits of DAST within the software development lifecycle.
* **Key Concepts:**
    * **Black-Box Testing:** DAST evaluates running web applications without requiring access to underlying source code or internal server configurations.
    * **Pros & Cons:**
        * **Pros:** Detects runtime issues, environment misconfigurations, and authentication flaws; produces low false-positive rates because vulnerabilities are observed in execution.
        * **Cons:** Cannot pinpoint exact source code line numbers; requires a fully deployed, running environment to execute scans.

## Task 3: Spiders and Crawlers
* **Overview:** Covers how DAST tools map out an application's attack surface using automated web crawling and spidering mechanisms.
* **Key Mechanics:**
    * **Traditional Spidering:** Parses HTML responses to discover internal links, forms, and endpoints across static assets.
    * **AJAX / Dynamic Crawling:** Uses headful or headless browser automation (e.g., Selenium, Puppeteer) to execute JavaScript and map dynamic client-side single-page applications (SPAs).

## Task 4: Scanning for Vulnerabilities
* **Overview:** Explores how active and passive scanners identify security flaws across mapped application routes.
* **Key Concepts:**
    * **Passive Scanning:** Inspects HTTP requests and responses (headers, cookies, body text) without sending malicious payloads or altering application traffic.
    * **Active Scanning:** Sends functional attack payloads (e.g., XSS, SQLi, command injection) to endpoints and parameters to analyze runtime behavior and error responses.

## Task 5: Authenticated Scans
* **Overview:** Demonstrates how to configure `OWASP ZAP` to record login flows and maintain active sessions to test protected endpoints behind authentication.
* **Key Steps & Mechanisms:**
    * **ZEST Scripts:** Used to record and replay HTTP authentication requests.
    * **Context & User Setup:** Defining target scope URLs in ZAP contexts and creating active user profiles to trigger authenticated scans.
    * **Session Maintenance:** Defining "Logged-in" and "Logged-out" indicators (HTML snippets or strings) and setting verification strategies to automatically re-authenticate if a session expires.
    * **Excluding Endpoints:** Marking scripts like `logout.php` to prevent ZAP from ending its own session during spidering.

## Task 6: Checking APIs with ZAP
* **Overview:** Explores scanning web Application Programming Interfaces (APIs)—such as REST or OpenAPI/Swagger endpoints—using ZAP.
* **Key Concepts:**
    * **Importing Definitions:** Loading API specifications (OpenAPI/Swagger, GraphQL, or WSDL) into ZAP to automatically discover endpoints and input parameters without needing a web crawler.
    * **Fuzzing & Active Scanning:** Injecting test payloads into API request parameters, headers, and JSON/XML bodies to test for vulnerabilities like injection, broken object-level authorization, and rate-limiting flaws.

## Task 7: Integrating DAST into the Development Pipeline
* **Overview:** Focuses on automating DAST tools within Continuous Integration and Continuous Deployment (CI/CD) pipelines to enforce continuous security testing.
* **Key Automation Strategies:**
    * **ZAP Automation Framework / Baseline Scans:** Running lightweight, containerized ZAP Docker scans (e.g., `zap-baseline.py` or GitHub Actions) during automated build and release stages.
    * **Automated Quality Gates:** Setting pass/fail thresholds based on vulnerability severity (e.g., breaking the build if high-risk alerts are detected).

## Task 8: Conclusion
* **Overview:** Wraps up the room by summarizing how DAST fits into the overall application security lifecycle.
* **Key Takeaways:**
    * DAST is vital for uncovering real-world, runtime security issues and environment misconfigurations in live environments.
    * A robust application security posture combines SAST early in development with DAST automated in pipelines and verified on live deployments.