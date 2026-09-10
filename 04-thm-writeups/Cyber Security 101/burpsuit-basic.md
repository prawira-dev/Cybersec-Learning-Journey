# Burp Suite: The Basics
## Intro
* **Overview:** Introduces Burp Suite as an essential web application security testing framework, outlining foundational concepts before moving into practical pentesting rooms.
* **Key Learning Objectives:**
    * A thorough introduction to what Burp Suite is and its core role in security testing.
    * An overview of the various tools available within the framework.
    * Guidance on installing Burp Suite on local system.
    * Instructions on navigating and configuring the interface.
    * An introduction to the Burp Proxy, which serves as the core component of the framework for intercepting and modifying web traffic

## What is Burp Suite 
* **Overview:** Introduces Burp Suite as a Java-based, industry-standard framework used for conducting manual and automated web application and API penetration testing by intercepting and manipulating HTTP/HTTPS traffic.

![burpsuit](../images/burpsuit.png)

* **Editions of Burp Suite:**
    * Burp Suite Community Edition: A free, local version for non-commercial use, ideal for learning manual security testing and core proxy features.
    * Burp Suite Professional: A paid, unrestricted version packed with advanced features like an automated vulnerability scanner, an unthrottled fuzzer/brute-forcer, session state saving, an API for tool integration, and Burp Collaborator.
    * Burp Suite Enterprise: A server-based edition designed for automated, continuous vulnerability scanning across web applications.

![burpsuit](../images/burpsuit-ent.png)

## Features of Burp Community
* ***Overview:*** Explores the powerful suite of built-in tools included in the free Community Edition of Burp Suite, highlighting how each module assists during web application security testing.
* **Core Features & Tools:**
    * **Proxy:** The flagship feature that enables real-time interception, inspection, and modification of HTTP/HTTPS requests and responses between the client and the target.
    * **Repeater:** Captures a request and allows you to modify and resend it multiple times, making it ideal for manual payload crafting, parameter testing, and vulnerability triage.
    * **Intruder:** Used for automated request spraying, fuzzing parameters, and performing brute-force attacks against target endpoints.
    * **Decoder:** Provides efficient data transformation capabilities, allowing you to encode or decode payloads and captured data on the fly.
    * **Comparer:** Facilitates byte-level or word-level comparison of two sets of data or responses to quickly spot differences.
    * **Sequencer:** Analyzes the randomness and entropy of supposedly unpredictable tokens (like session IDs or cookies) to uncover weak generation algorithms.
* **Extensions & Customization:** Burp Suite’s Java architecture supports third-party modules through the BApp Store and the Extender module (using Java, Jython for Python, or JRuby for Ruby) to enhance functionality, with useful plugins like Logger++.

## Installation
* Overview: Explores how to download and install Burp Suite across different operating systems to set up testing environment.
* Platform-Specific Installation:
    * AttackBox: If you use the TryHackMe AttackBox, Burp Suite is pre-installed, allowing you to skip the installation process entirely.
    * Kali Linux: Burp Suite comes pre-installed by default, but it can also be easily installed or updated via the Kali `apt` repositories.
    * Linux, macOS, and Windows: Dedicated installers for Burp Suite Community and Professional editions can be downloaded directly from the PortSwigger website. On Linux, running the installer script without `sudo` installs it locally in home directory (`~/BurpSuiteCommunity/BurpSuiteCommunity`) without adding it to system `PATH`.

## The Dashboard
* **Overview:** Explores the layout and function of the Burp Suite Dashboard, which appears after configuration and serves as the central hub for monitoring background activities and system status.
* **Four Quadrants of the Dashboard:**
    * **Tasks:** Manages background tasks performed by Burp Suite, such as the default "Live Passive Crawl" in the Community Edition that automatically logs visited pages.
    * **Event Log:** Records actions performed by Burp Suite—such as starting the proxy or logging connection details.
    * **Issue Activity:** Exclusive to Burp Suite Professional, this section lists vulnerabilities discovered by the automated scanner, categorized by severity and certainty.
    * **Advisory:** Provides detailed information, references, and remediation guidance for identified vulnerabilities (which may be empty in the Community Edition).
* **Help Resources:** Highlights the question mark icons (`?`) scattered throughout Burp Suite's interface, which open helpful context-specific documentation and guides.

## Navigation
* **Overview:** Explores how to navigate Burp Suite's interface effectively using its top-level menu bars, sub-tabs, window management options, and keyboard shortcuts.
* **Module Selection & Sub-Tabs:**
    * The top row of the menu bar displays primary modules (such as Dashboard, Target, Proxy, Intruder, and Repeater) which you can click to switch between tools.
    * A second menu bar directly below displays module-specific sub-tabs (such as Intercept, HTTP history, WebSockets history, and Proxy settings within the Proxy module).
* **Detaching Tabs:** You can detach individual tabs into separate windows by navigating to the Window menu at the top and selecting the "Detach" option for the desired tab, allowing you to view multiple tools simultaneously.
* **Keyboard Shortcuts:** Burp Suite provides built-in shortcuts to quickly switch between essential tabs without using the mouse:
    * `Ctrl + Shift + D` $\rightarrow$ Dashboard
    * `Ctrl + Shift + T` $\rightarrow$ Target tab
    * `Ctrl + Shift + P` $\rightarrow$ Proxy tab
    * `Ctrl + Shift + I` $\rightarrow$ Intruder tab
    * `Ctrl + Shift + R` $\rightarrow$ Repeater tab

## Options
* **Overview:** Explores Burp Suite's centralized configuration options, which allow you to customize behavior, manage tool parameters, and adjust environments using two distinct settings scopes.
* **Settings Categories:**
    * Global Settings (User Settings): Affect the entire Burp Suite application installation and persist across every session and restart.
    * Project Settings: Apply exclusively to the current workspace session. Note that because the Community Edition does not support saving projects, any custom project settings are lost when Burp is closed.
* **The Settings Interface:** Accessed via the Settings button on the top navigation bar, the interface features a left-hand navigation pane categorized by tools (like Proxy, Intruder, Repeater), sessions, network settings, and user interface preferences. It also includes a handy keyword search bar and a type filter (All, User, Project) to help quickly locate specific configuration options.

## Introduction to the Burp Proxy
* **Overview:** Introduces the Burp Proxy as the cornerstone tool of Burp Suite, acting as a middleman to capture, inspect, and modify HTTP/HTTPS traffic between client browser and the target web server.
* **Key Capabilities:**
    * **Intercepting Requests:** Holds back requests from reaching the target server so you can analyze, edit, drop, forward, or send them to other Burp modules. You can toggle this on or off using the Intercept is on button.
    * **Default Logging & Capture:** Automatically logs all passed requests and responses in the background (even when interception is turned off), which can be reviewed in the HTTP history and WebSockets history sub-tabs.
* **Response Interception:** Allows you to configure custom rules to catch and modify server responses before they load in the browser.
* **Match and Replace:** Uses regular expressions (regex) to dynamically alter incoming or outgoing request parameters, headers, user agents, or cookies on the fly.

## Connecting through the Proxy (FoxyProxy)
* **Overview:** Focuses on configuring a local web browser to route traffic through the Burp Suite Proxy using the FoxyProxy browser extension in Firefox.
* **Configuration Steps:**
    * **Install FoxyProxy:** Download and install the FoxyProxy Basic extension (pre-installed on the TryHackMe AttackBox).
    * **Add Proxy Details:** Open FoxyProxy Options, click Add, and configure the proxy profile with the title `Burp`, Proxy IP `127.0.0.1`, and Port `8080`.
    * **Activate Configuration:** Click the FoxyProxy icon in the toolbar and select the Burp profile to direct browser traffic through `127.0.0.1:8080`.
* **Testing and Interception:**
    * Ensure Burp Suite is running and Intercept is turned on under the Proxy tab.
    * Accessing a target site (like `http://MACHINE_IP/`) will cause the browser to hang as the request is caught by the proxy.
    * Right-clicking the intercepted request allows you to forward, drop, or send it to other Burp tools.
* **Key Reminder:** Be cautious not to leave interception switched on unintentionally, as it will prevent browser from loading normal pages.

## Site Map and Issue Definitions
* **Overview:** Explores the Target tab in Burp Suite, which provides comprehensive tools for mapping web applications, defining testing scopes, and referencing vulnerability definitions.
* **Three Core Sub-Tabs of Target:**
    * **Site map:** Automatically builds a hierarchical tree structure of the target web application as you browse through the proxy. It captures every visited page, folder, file, and API endpoint, helping with enumeration and discovery.
    * **Issue definitions:** Provides a comprehensive dictionary of vulnerabilities that Burp Suite tests for, complete with detailed descriptions, remediation guidance, and references. This is useful for writing security reports or understanding discovered flaws.
    * **Scope settings:** Allows you to explicitly include or exclude specific domains and IPs, ensuring proxy captures only the traffic relevant to target and ignores background noise.
* **Practical Challenge:** The task instructs you to browse the target application with the proxy enabled, explore all linked pages, and check  Site map in Burp Suite to find an unusual endpoint containing a hidden flag.

## The Burp Suite Browser
* **Overview:** Introduces Burp Suite’s built-in Chromium browser, which comes pre-configured to route all traffic through the Burp Proxy automatically without needing external browser extensions or manual system proxy settings.
* **Usage:** To launch the built-in browser, simply click the Open browser button located under the **Proxy** → **Intercept tab** in Burp Suite.
* **Running as Root (AttackBox Limitation):** Because running Burp Suite as the root user on Linux (common in the TryHackMe AttackBox) prevents Chromium's sandbox from initializing, you can bypass the sandbox restriction by navigating to **Settings** → **Tools** → **Burp's browser** and checking the option **Allow Burp's browser to run without a sandbox**. (Note: This is safe in a lab environment but disabled by default for production security reasons).

## Scoping and Targeting
* **Overview:** Explores how to use Scoping in Burp Suite to filter out background noise and focus your proxy traffic exclusively on the target web application you want to test.
* **Adding a Target to Scope:**
    * Navigate to the Target tab, right-click your target from the site map list on the left, and select Add To Scope.
    * Burp Suite will prompt you to stop logging out-of-scope items, which you should generally confirm by selecting Yes.
    * Managing Scope Settings: You can review, fine-tune, add, or exclude specific domains and IPs by navigating to the Scope settings sub-tab within the Target tab.
* **Filtering Proxy Interception:** By default, the proxy still intercepts out-of-scope traffic even if logging is disabled. To fix this and prevent unrelated background requests from hanging your browser, go to the Proxy settings sub-tab and select And URL Is in target scope under the "Intercept Client Requests" section.

## Proxying HTTPS
* **Overview:** Explores how to handle HTTPS traffic in Burp Suite by trusting the PortSwigger Certificate Authority (CA) certificate, allowing the proxy to inspect encrypted traffic without throwing security warnings.
* **The Certificate Problem:** When intercepting HTTPS traffic (like [Google.com](https://google.com/)), browsers throw a security error because the traffic is signed by Burp Suite's custom CA rather than a recognized public authority.
* **Step-by-Step Configuration:**
    * Download the CA Certificate: With the Burp Proxy active, navigate to `http://burp/cert` in your browser to download the cacert.der certificate file.
    * Access Certificate Settings: Open Firefox preferences (`about:preferences`), search for "certificates", and click View Certificates.
    * Import the Certificate: Click Import, select the downloaded cacert.der file, and check the box to "Trust this CA to identify websites".
* **Result:** Once trusted, your browser will seamlessly accept the PortSwigger certificate, enabling safe and uninterrupted HTTPS interception and analysis through the Burp Proxy.

## Example Attack
* **Overview:** Provides a practical, real-world walkthrough of using the Burp Proxy to bypass client-side input filters and execute a Reflected Cross-Site Scripting (XSS) attack against a support form.
* **The Problem:** The target support page at `http://MACHINE_IP/ticket/` contains a client-side filter that prevents users from typing special characters (like `<` or `>`) required for scripting payloads into the "Contact Email" field.
* **Step-by-Step Walkthrough:**
    * **Enable Proxy Interception:** Ensure Burp Suite's proxy is running and Intercept is on.
    * Submit Legitimate Data: Type safe placeholder data into the form (e.g., `pentester@example.thm` and a query) and submit it, allowing Burp to catch the outgoing request.
    * **Inject the Payload:** In the Burp intercept window, replace the email parameter value with the XSS payload: `<script>alert("Succ3ssful XSS")</script>`.
    * **URL Encode:** Highlight the newly pasted payload text and press `Ctrl + U` to URL-encode the special characters so the web server can process them safely.
    * **Forward Request:** Click the **Forward** button to send the modified request to the server, triggering an alert box on the target page confirming a successful XSS execution.