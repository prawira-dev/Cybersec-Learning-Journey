# Metasploit: Introduction

## Main Component
* **Exploit:** A piece of code that uses a vulnerability present on the target system.
* **Vulnerability:** A design, coding, or logic flaw affecting the target system. The exploitation of a vulnerability can result in disclosing confidential information or allowing the attacker to execute code on the target system.
* **Payload:** the code that will run on the target system.

### Auxiliary
Any supporting module, such as scanners, crawlers and fuzzers, can be found here.
Example:
```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 auxiliary/
auxiliary/
├── admin
├── analyze
├── bnat
├── client
├── cloud
├── crawler
├── docx
├── dos
├── example.py
├── example.rb
├── fileformat
├── fuzzers
├── gather
├── parser
├── pdf
├── scanner
├── server
├── sniffer
├── spoof
├── sqli
├── voip
└── vsploit

20 directories, 2 files
```

### Encoders
Encoders will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them.
```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 encoders/
encoders/
├── cmd
├── generic
├── mipsbe
├── mipsle
├── php
├── ppc
├── ruby
├── sparc
├── x64
└── x86

10 directories, 0 files
```

### Evasion
While encoders will encode the payload, they should not be considered a direct attempt to evade antivirus software. On the other hand, “evasion” modules will try that, with more or less success.
```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 2 evasion/
evasion/
└── windows
    ├── applocker_evasion_install_util.rb
    ├── applocker_evasion_msbuild.rb
    ├── applocker_evasion_presentationhost.rb
    ├── applocker_evasion_regasm_regsvcs.rb
    ├── applocker_evasion_workflow_compiler.rb
    ├── process_herpaderping.rb
    ├── syscall_inject.rb
    ├── windows_defender_exe.rb
    └── windows_defender_js_hta.rb

1 directory, 9 files
```

### Exploits
Exploits, neatly organized by target system.
```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 exploits/
exploits/
├── aix
├── android
├── apple_ios
├── bsd
├── bsdi
├── dialup
├── example_linux_priv_esc.rb
├── example.py
├── example.rb
├── example_webapp.rb
├── firefox
├── freebsd
├── hpux
├── irix
├── linux
├── mainframe
├── multi
├── netware
├── openbsd
├── osx
├── qnx
├── solaris
├── unix
└── windows

20 directories, 4 files
```
### NOPs
NOPs (No OPeration) do nothing, literally. They are represented in the Intel x86 CPU family with 0x90, following which the CPU will do nothing for one cycle. They are often used as a buffer to achieve consistent payload sizes.
```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 nops/
nops/
├── aarch64
├── armle
├── cmd
├── mipsbe
├── php
├── ppc
├── sparc
├── tty
├── x64
└── x86

10 directories, 0 files
```
### Payloads
Payloads are codes that will run on the target system.

```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 payloads/
payloads/
├── adapters
├── singles
├── stagers
└── stages

4 directories, 0 files
```

* **Adapters:** An adapter wraps single payloads to convert them into different formats. For example, a normal single payload can be wrapped inside a Powershell adapter, which will make a single powershell command that will execute the payload.
* **Singles: **Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run.
* **Stagers:** Responsible for setting up a connection channel between Metasploit and the target system. Useful when working with staged payloads. “Staged payloads” will first upload a stager on the target system then download the rest of the payload (stage). This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.
* **Stages:** Downloaded by the stager. This will allow you to use larger sized payloads.

Metasploit has a subtle way to help you identify single (also called “inline”) payloads and staged payloads.
* generic/shell_reverse_tcp
* windows/x64/shell/reverse_tcp
Both are reverse Windows shells. The former is an inline (or single) payload, as indicated by the “_” between “shell” and “reverse”. While the latter is a staged payload, as indicated by the “/” between “shell” and “reverse”.

### Post
Post modules will be useful on the final stage of the penetration testing process listed above, post-exploitation.
```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 post/
post/
├── aix
├── android
├── apple_ios
├── bsd
├── firefox
├── hardware
├── linux
├── multi
├── networking
├── osx
├── solaris
└── windows

12 directories, 0 files
```

## Msfconsole
Launch it using the `msfconsole` command on your AttackBox terminal or any system the Metasploit Framework is installed on.

### **1. Metasploit Prompts & Contexts**

* *Command Prompts*: Metasploit uses distinct prompts depending on your current state:
    * System Prompt `root@ip...` : Standard OS command line where Metasploit commands cannot be used.
    * Console Prompt `msf6 >` : Main Metasploit prompt without an active module context.
    * Context Prompt `msf6 exploit(...) >` : Active prompt after selecting a module, allowing module-specific configuration.
    * Meterpreter Prompt `meterpreter >`: Interactive agent shell established on the target after a successful exploit.
    * Target Shell `C:\Windows\system32`>: Direct command shell on the exploited system.

### **2. Module Configuration & Parameters**
* Parameters are set using the syntax set `PARAMETER_NAME VALUE`.
* Common parameters include:
    * RHOSTS / RPORT: Target host IP (supports single IPs, CIDR ranges, or file lists) and remote port.
    * LHOST / LPORT: Attacking machine IP and listening port for reverse connections
    * PAYLOAD / SESSION: The payload to deliver or the session ID for post-exploitation modules.
* Global Variables (setg): Sets a parameter globally across all modules so values do not reset when switching contexts.
* Use `unset` or `unset all` to clear specific or all configured parameters.

### **3. Execution & Session Management**

* **Execution:** Run modules using exploit or run (common for scanners/auxiliary modules). Using exploit -z executes the exploit and immediately sends the created session to the background.
* **Checking Vulnerabilities:** Some modules support the check command to test if a target is vulnerable without launching an exploit.
* **Backgrounding & Sessions:** Active target connections form sessions. Use the background command or CTRL+Z to detach from an active Meterpreter prompt, and run sessions from the main prompt to view or interact with open channels.