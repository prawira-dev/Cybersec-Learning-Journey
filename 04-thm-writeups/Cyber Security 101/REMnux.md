# REMnux: Getting Started
## Intro
* **Overview:** Introduces the REMnux VM, a specialized Linux distribution specifically designed to provide a safe, sandbox-like environment for dissecting potentially malicious software without risking your primary system.
* **Built-in Capabilities:** The distribution comes pre-configured with a suite of essential analysis tools, eliminating the hassle of manual lab setup. Highlighted tools include Volatility, YARA, Wireshark, oledump, and INetSim.
* **Learning Objectives:** The room covers exploring the built-in tools, analyzing potentially malicious documents, simulating fake networks to observe malware behavior, and preprocessing memory images for investigation.
* **Prerequisites:** Recommends familiarizing yourself with the CyberChef: The Basics room before starting.

## Machine Access
* **Overview:** Explains how to initialize and connect to the REMnux virtual environment required for the REMnux: Getting Started room's exercises.
* **Lab Initialization:** Start the attached lab machine, which will boot into a split-screen view alongside the TryHackMe instructions (taking roughly 2-3 minutes). If the VM does not automatically appear, you can manually reveal it by clicking the Show Split View button at the top of the page.
* **Working Directory:** All the sample files and malicious artifacts used throughout the room's upcoming tasks are centrally located in the Desktop/tasks directory on the virtual machine.

## File Analysis
* **Overview:** Focuses on performing static analysis on a potentially malicious Excel document (agenttesla.xlsm) using the Python tool oledump.py to extract and examine embedded macros.
* **Tool Execution:**
    * **Listing Streams:** Running `oledump.py agenttesla.xlsm` displays the file's data streams. Streams containing macros are marked with an `M`.
    * **Extracting Content:** To view a specific stream (like stream 4), use the `-s 4` parameter.
    * **Decompressing:** Adding the `--vbadecompress` flag translates the raw hex dump into readable VBA macro code.
    * **Deobfuscation:** The extracted VBA macro contains an obfuscated PowerShell payload. By using CyberChef's Find/Replace operations, analysts can strip away junk characters (like * and ^) to reveal the true script.
    * **Script Analysis:** The deobfuscated script reveals classic malware deployment techniques:
        * `-WindowStyle hidden`: Hides the terminal from the user.
        * `-executionpolicy bypass`: Overrides script execution restrictions.
        * `Invoke-WebRequest`: Downloads the malicious payload from an external IP.
        * `Start-Process`: Executes the downloaded binary.

## Fake Network to Aid Analysis
* **Overview:** Focuses on dynamic analysis by simulating a live network environment using INetSim (Internet Services Simulation Suite) within the REMnux VM. This allows analysts to safely observe how malware behaves on a network, such as attempting to contact Command and Control (C2) servers or downloading secondary payloads.
* **Configuration & Setup:**
    * First, determine the REMnux VM's IP address using `ifconfig`.
    * Edit the INetSim configuration file (sudo nano /etc/inetsim/inetsim.conf) to uncomment and change `dns_default_ip` from `0.0.0.0` to your REMnux machine's IP.
    * Launch the simulation by running `sudo inetsim`.
* **Simulating Malware Behavior:** Using the AttackBox, you mimic malicious activity by reaching out to the REMnux IP. By running commands like `sudo wget https://[MACHINE_IP]/second_payload.zip --no-check-certificate`, you trigger INetSim to serve a safe, fake file in place of a real malicious payload.
* **Analyzing the Connection Report:** Once the simulation is stopped, INetSim generates a detailed report (saved in `/var/log/inetsim/report/`). Reading this report reveals exactly what the "malware" tried to do, including the specific URLs it attempted to reach, the protocols used, and the HTTP request methods.

## Memory Investigation: Evidence Preprocessing
* **Overview:** Focuses on the crucial digital forensics step of preprocessing evidence, which involves extracting specific artifacts from memory images and saving them for analysis.
* **The Tool:** Utilizes the Volatility 3 framework, which is pre-installed on the REMnux VM.
* **Target File:** The exercises revolve around analyzing a memory dump named `wcry.mem` located in the `/home/ubuntu/Desktop/tasks/Wcry_memory_image/` directory.
* **Key Volatility Plugins Used:**
    * `windows.pstree.PsTree`: Displays active processes in a hierarchical tree based on their Parent Process ID (PPID).
    * `windows.pslist.PsList`: Lists all currently active processes running on the machine.
    * `windows.cmdline.CmdLine`: Extracts and lists the command-line arguments used to launch processes.
    * `windows.filescan.FileScan`: Scans the memory image for file objects to see what files were present or open.
    * `windows.dlllist.DllList`: Lists the dynamic-link libraries (DLLs) loaded by a specific process.
    * `windows.malfind.Malfind`: Identifies potentially injected or hidden code within active processes.