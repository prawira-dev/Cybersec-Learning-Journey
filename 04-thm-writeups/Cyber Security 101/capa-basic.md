# CAPA: The Basics
## Intro
* **Overview:** Introduces CAPA (Common Analysis Platform for Artifacts), a static analysis tool developed by the FireEye Mandiant team. It is designed to identify the capabilities of potentially malicious software without needing to execute the files in a dynamic sandbox.
* **Core Function:** Automatically analyzes executable files (such as PE, ELF, .NET modules, and shellcode) against a set of rules describing common behaviors. It identifies what a program is capable of doing, including network communication, file manipulation, and process injection, effectively automating years of reverse engineering knowledge.
* **Learning Objectives:** The room aims to teach how to use CAPA effectively, dissect its results (including MITRE and MAEC mappings), and identify a program’s potential malicious activities.
* **Lab Environment:** A Windows virtual machine is provided with CAPA pre-installed. Because CAPA scans can be time-consuming, pre-processed reports (such as cryptbot.txt and cryptbot_vv.json) are readily available on the Administrator desktop for analysis.

## Tool Overview: How CAPA Works
* **Overview:** Demonstrates the basic usage and command-line execution of CAPA to analyze an executable (like cryptbot.bin) directly from the PowerShell terminal.
* **Execution:** To run the tool, navigate to the directory containing the binary and execute it by pointing to the file (e.g., `capa.exe .\cryptbot.bin`).
* **Key Parameters:**
    * `-h`: Displays the help message and available parameters.
    * `-v`: Enables verbose output for a more detailed results document.
    * `-vv`: Enables very verbose output to extract the deepest level of information regarding the malware's capabilities. Note that increasing verbosity increases processing time.
* **Handling Long Scans:** Because live scanning can take several minutes, the room provides pre-processed outputs that can be viewed immediately using native PowerShell commands like `Get-Content cryptbot.txt`.

## Dissecting CAPA Results Part 1: General Information, MITRE and MAEC
* **Overview:** Breaks down the initial sections of CAPA's output, which categorizes a malware sample's basic properties and maps its behavior to standardized security frameworks.
* **General Information:** The first block of the CAPA report provides basic file details, including cryptographic hashes (MD5, SHA1/256), the operating system context, file format (e.g., PE), and the target architecture (e.g., x86/i386).
* **MITRE ATT&CK Mapping:** CAPA automatically maps the file's identified capabilities to the MITRE ATT&CK framework, categorizing behaviors by Tactics (the attacker's goal), Techniques (how they achieve it), Sub-Techniques, and specific Identifiers (e.g., T1027 for Obfuscated Files or Information).
* **MAEC (Malware Attribute Enumeration and Characterization):** CAPA uses this standardized language to tag the overall category of the malware. Common MAEC values include:
    * **Launcher:** Exhibits behaviors like dropping additional payloads, activating persistence, or connecting to C2 servers.
    * **Downloader:** Exhibits behaviors like fetching additional payloads from the internet, pulling updates, or retrieving configuration files.

## Dissecting CAPA Results Part 2: Malware Behavior
* **Overview:** Explores the Malware Behavior Catalogue (MBC), which serves as a standardized directory of malware objectives and behaviors. It complements the MITRE ATT&CK framework but is tailored specifically for malware analysis and reverse engineering contexts.
* **Core Concepts:**
    * **Objectives:** This field maps directly to ATT&CK tactics (e.g., Execution, Defense Evasion, Persistence) but frames them within the context of malware behavior. It also introduces malware-specific categories like Anti-Behavioral Analysis and Anti-Static Analysis.
    * **Micro-behaviors & Identifiers:** CAPA breaks down broader objectives into distinct, low-level actions called micro-behaviors, each assigned a specific identifier. For instance, specific tags are generated when a binary attempts to create a process, detect a virtual machine environment, or encode data.
* **Actionable Intelligence:** By highlighting micro-behaviors (such as identifying that the malware can initiate HTTP communications or obfuscate strings using Base64 and XOR), analysts gain a granular understanding of the malware's capabilities without needing to reverse-engineer the code manually.

## Dissecting CAPA Results Part 3: Namespaces
* **Overview:** Explores how CAPA categorizes and groups identified malware capabilities using Namespaces to make analyzing the tool's output easier and more structured.
* **Top-Level Namespaces (TLN):** Broad categories that group behaviors by their primary purpose. Key examples include:
    * **anti-analysis:** Rules designed to detect evasion techniques like obfuscation, packing, and anti-debugging.
    * **persistence:** Behaviors associated with maintaining access within a compromised system over an extended period.
    * **nursery:** A staging ground containing experimental or unpolished rules.
    * **data-manipulation, communication, impact:** Other TLNs covering data alteration, network activity, and potential harm, respectively.
* **Namespaces (Sub-categories):** More granular groupings nested within a TLN. For example, under the anti-analysis TLN, you will find:
    * **anti-vm/vm-detection:** Focuses specifically on identifying if the malware is looking for virtual machine environments (like VMware or VirtualBox).
    * **obfuscation:** Focuses on techniques like string encryption or code packing meant to conceal the program's true purpose.

## Dissecting CAPA Results Part 4: Capability
* **Overview:** Focuses on understanding the "Capability" column in CAPA's output and how it correlates with Namespaces and specific YAML rule files to pinpoint exact malware behaviors.
* **Capability to Rule Mapping:**
    * The name of an identified Capability (e.g., "reference anti-VM strings") translates directly to the name of its underlying YAML rule file (e.g., reference-anti-vm-strings.yml), with spaces simply replaced by hyphens.
    * Capabilities are categorized into specific Namespaces (e.g., anti-vm/vm-detection), which are grouped under broader Top-Level Namespaces (TLNs) like Anti-Analysis, Communication, or Data Manipulation.
    * This hierarchical structure allows analysts to quickly trace an identified behavior back to its exact detection logic.
* **The Nursery TLN:** Serves as a placeholder for experimental or unpolished rules. Occasionally, a capability that logically belongs in a definitive category (like "reference cryptocurrency strings" under the Impact TLN) may temporarily reside in the Nursery until it is fully refined.

## More Information, more fun!
* Overview: Focuses on extracting deep, granular details about exactly why a specific CAPA rule was triggered by utilizing very verbose outputs and interactive web-based analysis.
* **Deep Analysis Techniques:**
    * **Very Verbose Mode (`-vv`):** Running CAPA with this parameter reveals the exact conditions and string matches found within the analyzed file.
    * **JSON Export (`-j`):** Because verbose text outputs can span thousands of lines and are difficult to read in a terminal, analysts can export the results to a JSON file (e.g., `capa.exe -j -vv .\cryptbot.bin > cryptbot_vv.json`).
* **CAPA Web Explorer:** A browser-based GUI (available online or as a local HTML file) designed to ingest CAPA's JSON output. It transforms the overwhelming raw data into an interactive, easy-to-navigate dashboard. LINK: [CAPA Web Explorer](https://mandiant.github.io/capa/explorer/#/)
    * **Rule Features:** The explorer allows you to view the exact YAML rule configuration and the specific features (like regex strings `/VMWare/i` or `/schtasks/i`) that matched the file's contents.
    * **Global Search Box:** A built-in filtering tool within the Web Explorer that helps quickly search and sift through large amounts of rule data.
