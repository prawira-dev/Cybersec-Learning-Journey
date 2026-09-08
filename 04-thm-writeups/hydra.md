# Hydra
## Hydra Introduction
**Overview:** Introduces Hydra as a fast network logon cracker used to perform automated online brute-force attacks against various authentication services.
* **How It Works:** Rather than manually testing login credentials on services like SSH, FTP, or web forms, Hydra rapidly cycles through a list of usernames and passwords to determine valid credentials.
* **Supported Protocols:** Hydra supports a wide array of protocols and services, including SSH, FTP, Telnet, SMB, SMTP, RDP, MySQL, and various HTTP form-based login methods.
* **Security Takeaway:** Highlights the critical importance of using strong, complex, and unique passwords, as default credentials (like admin:password) and weak dictionary words are easily compromised by rapid online brute-force tools.

## Using Hydra
* **Overview:** Explores practical syntax and command structures for using Hydra to perform online brute-force attacks against target services, specifically focusing on SSH and HTTP POST login forms.
* **SSH Brute-Forcing Syntax:**
    * **Command structure:** `hydra -l <username> -P <full path to pass> <target-ip> -t <threads> ssh`
    * **Key flags:** 
        * `-l` specifies the username
        * `-P` points to the password wordlist
        * `-t` defines the number of parallel threads to speed up the process.
* **HTTP POST Web Form Brute-Forcing Syntax:**
    * Command structure: `hydra -l <username> -P <wordlist> <target-ip> http-post-form "<path>:<login_credentials>:<invalid_response>" -V`
    * **Key components:**
        * `http-post-form` targets POST-based login endpoints
        * `^USER^` and `^PASS^` placeholders map form fields, and the invalid response string (e.g., `:F=incorrect`) tells Hydra how to detect failed login attempts.
        * The `-V` flag enables verbose mode to show every attempt.
* **Practical Lab Challenge:** The task requires deploying the target machine's IP and using Hydra to crack credentials for the user molly across both the web login form (to capture Flag 1) and the SSH service (to capture Flag 2).

    * For web password
    ```
    hydra -l molly -P /usr/share/wordlists/rockyou.txt MACHINE_IP -f -t 4 ssh
    ```
    * For SSH
    ```
    hydra -l molly -P /usr/share/wordlists/rockyou.txt MACHINE_IP -f -t 4 ssh
    ```
> [!TIP]
> Use `-f` options to stop Hydra once a valid password is found, which can save time.