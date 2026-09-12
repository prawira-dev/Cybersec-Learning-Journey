# FlareVM: Arsenal of Tools
## Intro
* **Overview:** Introduces FlareVM (Forensics, Logic Analysis, and Reverse Engineering), a specialized security toolkit expertly curated by the FLARE Team at FireEye. It is tailored for reverse engineers, malware analysts, incident responders, and forensic investigators.
* **Learning Objectives:** The task sets the stage for exploring the FlareVM toolset, focusing on effectively analyzing potentially malicious processes and performing static analysis on suspicious documents and binaries.
* **Lab Environment Setup:** Building FlareVM from scratch takes hours, so the room provides a pre-configured lab machine accessible via split-screen or RDP (Credentials: `Administrator` / `letmein123!`). All required analysis files are located in the `C:\Users\Administrator\Desktop\Sample` directory.
* **Safety Disclaimer:** The attached machine contains live, malicious sample files for practical exercises. These files must remain securely isolated within the VM and should never be downloaded, distributed, or executed on your local machine.

## Arsenal of Tools
* **Overview:** Introduces the extensive suite of specialized tools pre-installed on FlareVM, grouping them by their primary use cases in forensics, incident response, and malware investigation.
* **Tool Categories:**
    * **Reverse Engineering & Debugging:** Tools like Ghidra, x64dbg, OllyDbg, and Radare2 for taking apart compiled code to understand its inner workings.
    * **Disassemblers & Decompilers:** Tools like CFF Explorer and RetDec for breaking malicious software into an understandable format.
    * **Static & Dynamic Analysis:** Utilities like Process Hacker and PEview for examining malware behavior without execution (static) or while it runs (dynamic).
    * **Forensics & Incident Response:** Frameworks like Volatility and FTK Imager for memory analysis and digital evidence preservation.
    * **Network Analysis:** Tools like Wireshark and Nmap for studying network traffic patterns.
    * **File Analysis:** Hex editors like HxD and FileInsight for examining and editing binary files.
    * **Scripting & Automation:** Python and PowerShell Empire for automating repetitive investigation tasks.
    * **Sysinternals Suite:** Windows management tools like Autoruns and Process Monitor for troubleshooting and tracking system activity.

## Commonly Used Tools for Investigation: Overview
* **Overview:** Details the practical functions of seven essential investigative tools featured on FlareVM that are used for initial malware triage and system analysis.
* **Key Investigative Tools:**
    * **Procmon (Process Monitor):** Tracks real-time system, file system, registry, and thread/process activity. Useful for observing how programs interact with the operating system.
    * **Process Explorer (Procexp):** Provides in-depth insight into running processes, detailing parent-child relationships, spawned programs, loaded DLLs, and associated user accounts.
    * **HxD:** A flexible hex editor used to inspect raw binary data, check file structures (such as identifying executable headers like `4D 5A`), and evaluate specific byte types using its Data Inspector.
    * **Wireshark:** Captures and analyzes network traffic to trace malicious connections, protocols, and data exfiltration patterns.
    * **CFF Explorer:** Inspects Portable Executable (PE) file headers, generates file hashes (like MD5 and SHA-1) for integrity verification, and checks the validity of system files.
    * **PEStudio:** Performs static analysis on executable properties without running the file, providing details such as entropy levels and indicators of potential packing or encryption.
    * **FLOSS (FLARE Obfuscated String Solver):** Automatically extracts and de-obfuscates static, stack, and tight strings from compiled binaries to uncover hardcoded URLs, IP addresses, API calls, and configuration data.

## Analyzing Malicious Files!
* **Overview:** A hands-on investigation task where you apply static and dynamic analysis techniques using FlareVM tools to dissect malicious executables (`windows.exe` and `cobaltstrike.exe`) located in `C:\Users\Administrator\Desktop\Sample`.
* **Static Analysis (PEStudio & FLOSS):**
    * **PEStudio:** Inspects executable properties without running the file. It evaluates file entropy, checks manifests for `requestedExecutionLevel`, identifies suspicious metadata (such as Russian strings in description fields indicating non-standard origins), uncovers missing rich headers, and lists imported APIs via the Import Address Table (IAT).
    * **FLOSS:** Extracts static and obfuscated strings from the binary to corroborate API calls and hardcoded indicators of compromise.
* **Dynamic Analysis (Process Explorer & Process Monitor):**
    * **Process Explorer:** Tracks running processes to map parent-child relationships, inspect process IDs, and check active network connections under the TCP/IP properties tab.
    * **Process Monitor (Procmon):** Records real-time system, file, and registry activity. By applying filters matching specific process names (e.g., `cobalt`), analysts can capture detailed telemetry confirming malicious outbound C2 network connections.