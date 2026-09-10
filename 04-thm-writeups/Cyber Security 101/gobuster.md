# Gobuster: The Basics
## Intro
* **Overview:** Introduces Gobuster as an essential offensive security tool used primarily for reconnaissance and enumeration.
* **Key Learning Objectives:**
    * Understanding the fundamental concepts of web enumeration.
    * Learning how to use Gobuster to find hidden web directories and files.
    * Using Gobuster to discover subdomains associated with a target.
    * Enumerating virtual hosts (vhosts) using the tool.
    * Leveraging wordlists effectively for brute-force discovery.

## Environment
* **Overview:** Details the lab environment setup for the room, which features an Ubuntu target web server running multiple subdomains, virtual hosts (vhosts), and two content management systems (WordPress and Joomla).
* **Lab Configuration Steps:**
    * Start the target lab machine and use the AttackBox (where Gobuster is pre-installed) to run enumeration commands.
    * Configure the local DNS resolver on the AttackBox by editing `sudo nano /etc/resolv-dnsmasq` to include the target machine's `MACHINE_IP` as the primary nameserver (`nameserver MACHINE_IP`).
    * Restart the Dnsmasq service using `/etc/init.d/dnsmasq restart` to ensure proper name resolution for the virtual hosts and subdomains hosted on the target.

## Gobuster: Intro
* **Overview:** Introduces Gobuster as a fast, open-source offensive enumeration tool written in Go, used primarily during the reconnaissance phase to find hidden web resources through brute-forcing.
* **Key Concepts:**
    * **Enumeration:** Listing all available resources on a target, whether they are publicly accessible or hidden.
    * **Brute-Forcing:** Iterating through wordlists to test every possible option until a match or valid endpoint is discovered.
* **Core Commands & Flags:**
    * `gobuster dir`: Enumerate web directories and files.
    * `gobuster dns`: Enumerate DNS subdomains.
    * `gobuster vhost`: Enumerate virtual hosts.
    * `-u`: Specifies the target URL.
    * `-w`: Specifies the path to the wordlist.
    * `-t`: Configures the number of concurrent threads to optimize scan speed.

## Use Case: Directory and File Enumeration
* **Overview:** Focuses on using Gobuster's dir mode to discover hidden web directories, file structures, and endpoint configurations using wordlist brute-forcing.
* **Core Command Syntax:**
    * `gobuster dir -u "[http://www.example.thm](http://www.example.thm)" -w /path/to/wordlist`
* **Essential Flags:**
    * ``-k`` / `--no-tls-validation`: Skips TLS certificate checks, commonly needed for self-signed certificates in CTF challenges.
    * `-x` / `--extensions`: Specifies file extensions to search for (e.g., .php, .js).
    * `-r` / `--follow-redirect`: Automatically follows HTTP redirection responses (like status codes 301 or 302).
    * `-s` / `--status-codes`: Filters results to display only specific HTTP status codes.
    * `-b` / `--status-codes-blacklist`: Excludes specific status codes from the output.
* **Key Concepts:**
    * Gobuster does not perform recursive scans by default, meaning any interesting directories discovered must be targeted and scanned individually.
    * Reviewing status codes helps quickly determine whether a resource is publicly accessible, requires authorization, or leads to a redirect.
```
gobuster dir -u http://www.offensivetools.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

## Use Case: Subdomain Enumeration
* **Overview:** Explores Gobuster's dns mode, which is used to brute-force subdomains of a target domain to uncover hidden or forgotten endpoints that may contain vulnerabilities.
* **Core Command Syntax:**
```
gobuster dns -d example.thm -w /path/to/wordlist
```
* **Essential Flags:**
    * `-d` / `--domain`: Configures the target domain you want to enumerate.
    * `-w`: Specifies the wordlist used to construct DNS queries.
    * `-i` / `--show-ips`: Displays the resolved IP addresses alongside discovered subdomains.
    * `-c` / `--show-cname`: Shows CNAME records (cannot be combined with the -i flag).
    * `-r` / `--resolver`: Sets a custom DNS server to use for resolution.
* **Key Concept:** Subdomains often run different applications or services than the main domain (e.g., development panels, login portals, or older APIs) and may lack the security patches applied to the primary site.

## Use Case: Virtual Host Enumeration
* **Overview:** Explores Gobuster's vhost mode, which is used to brute-force virtual hosts (multiple distinct websites or applications hosted on the same IP address and server).
* **Vhosts vs. Subdomains:** While subdomains are configured and resolved through DNS, virtual hosts are IP-based. Gobuster differentiates by sending HTTP requests with modified Host: headers for each entry in a wordlist.
* **Core Command Syntax:**
```
gobuster vhost -u "http://MACHINE_IP" --domain example.thm -w /path/to/wordlist --append-domain
```
* **Essential Flags:**
    * `-u` /`url` : Specifies the base URL of the target server.
    * `--domain`: Sets the target second-level and top-level domain.
    * `--append-domain`: Appends the base domain automatically to every word in the wordlist (e.g., combining blog with example.thm).
    * `--exclude-length`: Filters out responses based on specific body lengths, which is critical for screening out false-positive pages (such as uniform 404 error pages).
* **Key Concepts:**
    * The Host header in HTTP requests allows multiple domains to share a single IP address (Virtual Hosting).
    * Virtual hosts may have different content, permissions, or services exposed to users, making them valuable targets for enumeration.
    * Gobuster tests each wordlist entry as a Host header, checking if the server returns a different page than the default.

## Conclusion
* **Overview:** Wraps up the room by recapping the core offensive enumeration capabilities and operational modes of Gobuster.
* **Key Modes Covered:**
    * `dir mode`: Enumerates hidden web directories and files.
    * `dns mode`: Enumerates subdomains by leveraging DNS services with a configured domain and wordlist.
    * `vhost mode`: Enumerates virtual hosts by sending customized web requests (Host: headers) against a target URL and wordlist.
* **Summary Takeaway:** Re-emphasizes the importance of understanding both required configuration flags and optional fine-tuning parameters across all three modes to effectively map attack surfaces during reconnaissance.