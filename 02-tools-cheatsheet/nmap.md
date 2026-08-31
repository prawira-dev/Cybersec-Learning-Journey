# NMAP - Network Mapper Cheatsheet

## Introduction

**Nmap** (Network Mapper) is a powerful, open-source tool used for network exploration and security auditing. It is designed to rapidly scan large networks, although it works fine against single hosts. Nmap uses raw IP packets to determine what hosts are available on the network, what services those hosts are offering, and many other characteristics.

---

## Basic Syntax

```bash
nmap [Scan Type] [Options] [Target]
```

### Target Specification Examples
```bash
nmap example.com              # Single host
nmap 192.168.1.1              # Single IP
nmap 192.168.1.0/24           # Subnet
nmap 192.168.1.1-10           # Range
nmap -iL targets.txt          # From file
nmap --exclude 192.168.1.5    # Exclude hosts
```

---

## Scan Types

### TCP Scan Types

| Option | Description | Privileges |
|--------|-------------|-----------|
| `-sS` | **SYN Scan** (Stealth Scan) - Default for root users. Performs a half-open connection | Root |
| `-sT` | **TCP Connect Scan** - Full three-way handshake. Default for non-root users | User |
| `-sA` | **TCP ACK Scan** - Firewall rule mapping, not for port discovery | Root |
| `-sW` | **TCP Window Scan** - Examines window field in TCP response packets | Root |
| `-sM` | **TCP Maimon Scan** - Uses FIN/ACK probes for BSD systems | Root |

### UDP Scan Types

| Option | Description |
|--------|-------------|
| `-sU` | **UDP Scan** - Scans UDP ports for open services |

### Advanced Scan Types

| Option | Description | Privileges |
|--------|-------------|-----------|
| `-sN` | **Null Scan** - No TCP flags set | Root |
| `-sF` | **FIN Scan** - Only FIN flag set | Root |
| `-sX` | **Xmas Scan** - FIN, PSH, and URG flags set | Root |
| `-sI <zombie>` | **Idle/Zombie Scan** - Uses a third-party host | Root |

---

## Port Specification

```bash
nmap -p 80              # Single port
nmap -p 80,443          # Multiple ports
nmap -p 1-1000          # Port range
nmap -p-                # All 65535 ports
nmap -p U:53,T:22       # UDP port 53 and TCP port 22
nmap --top-ports 100    # Scan top 100 most common ports
```

---

## Host Discovery (Ping Sweep)

| Option | Description |
|--------|-------------|
| `-sn` | Ping scan - Disable port scanning, only host discovery |
| `-Pn` | Treat all hosts as online - Skip ping, assume host is up |
| `-PE` | ICMP Echo requests |
| `-PP` | ICMP Timestamp requests |
| `-PM` | ICMP Address mask requests |
| `-PB` | ICMP Ping and TCP ACK ping (default) |
| `-PS[ports]` | TCP SYN ping on port 80 by default |
| `-PA[ports]` | TCP ACK ping |
| `-PU[ports]` | UDP ping |

---

## Service and Version Detection

```bash
nmap -sV                          # Probe open ports to determine service versions
nmap -sV --version-intensity 9    # Maximum intensity version detection
nmap -sC                          # Run default NSE scripts
nmap -sV -sC                      # Combined service detection and scripts
```

---

## OS Detection

```bash
nmap -O                    # Enable OS detection
nmap -O --osscan-limit    # OS detection only for promising targets
nmap -O --osscan-guess    # Guess OS if not confident
```

---

## Timing and Performance

| Option | Description |
|--------|-------------|
| `-T0` | **Paranoid** - Very slow, IDS evasion |
| `-T1` | **Sneaky** - Slow, IDS evasion |
| `-T2` | **Polite** - Slower to avoid network load |
| `-T3` | **Normal** - Default timing |
| `-T4` | **Aggressive** - Faster, assumes good network |
| `-T5` | **Insane** - Very fast, assumes excellent network |
| `--min-rate <number>` | Minimum packets/second |
| `--max-rate <number>` | Maximum packets/second |

---

## NSE (Nmap Scripting Engine)

```bash
nmap --script default                    # Run default scripts
nmap --script vuln                       # Run vulnerability assessment scripts
nmap --script http-title                 # Specific script
nmap --script "http-*"                   # Wildcard pattern
nmap --script-args "arg1=value1"         # Pass arguments to scripts
nmap --script-updatedb                   # Update NSE script database
```

### Common Script Categories
- `default` - Safe scripts, useful information
- `vuln` - Vulnerability detection
- `safe` - Safe scripts
- `discovery` - Service discovery
- `intrusive` - May crash services or affect targets

---

## Output Options

```bash
nmap -oN output.txt          # Normal output format
nmap -oX output.xml          # XML output format
nmap -oG output.gnmap        # Greppable output format
nmap -oA output              # All three formats
nmap -v                      # Increase verbosity
nmap -vv                     # Very verbose
nmap -d                      # Debugging output
nmap -dd                     # Higher debugging level
```

---

## Common Scanning Combinations

### Aggressive Scan
```bash
nmap -A <target>
# Equivalent to: -sV -sC -O --traceroute
# Detects services, runs scripts, and OS detection
```

### Comprehensive Network Audit
```bash
nmap -sV -sC -O -A -T4 -p- <target>
# Full port scan with service detection, scripts, and OS detection
```

### Quick Scan
```bash
nmap -F <target>
# Scan fewer ports for speed (common ports only)
```

### Stealth Scan
```bash
nmap -sS -T1 -f --decoy <decoy1>,<decoy2> <target>
# Fragmented packets with decoys for stealth
```

### Intense Scan
```bash
nmap -p 1-65535 -T4 -sV -sC --version-all <target>
# Scan all ports with detailed detection
```

---

## Useful Options

| Option | Description |
|--------|-------------|
| `-6` | IPv6 scanning |
| `-f` | Fragment packets |
| `--mtu <value>` | Specify MTU size |
| `--source-port <port>` | Spoof source port |
| `--data-length <size>` | Append random bytes to packets |
| `-D <decoy1>,<decoy2>` | Use decoy hosts |
| `--reason` | Show reason for port state |
| `--open` | Show only open ports |
| `-S <spoofed_IP>` | Spoof source IP address |
| `-g <port>` | Use given source port |
| `--dns-servers <server>` | Use custom DNS servers |

---

## Firewall/IDS Evasion

```bash
nmap -f -T1 --randomize-hosts <target>
# Fragment packets, paranoid timing, randomized scan order

nmap -D RND:5 <target>
# Use 5 random decoys

nmap --badsum <target>
# Send packets with bad checksums (unreliable targets only)

nmap --spoof-mac 0 <target>
# Randomize MAC address
```

---

## Examples and Use Cases

### 1. Basic Host Discovery
```bash
nmap -sn 192.168.1.0/24
# Find all active hosts on the network
```

### 2. Scan Specific Ports
```bash
nmap -p 22,80,443 example.com
# Check if SSH, HTTP, and HTTPS are open
```

### 3. Full Service Enumeration
```bash
nmap -sV -sC -A example.com
# Comprehensive service and vulnerability detection
```

### 4. UDP Service Detection
```bash
nmap -sU -p 53,123,161 example.com
# Scan for DNS, NTP, and SNMP
```

### 5. OS and Version Detection
```bash
nmap -O -sV example.com
# Determine operating system and service versions
```

### 6. Save Results for Later Review
```bash
nmap -A -oA scan_results example.com
# Output in all formats for comprehensive analysis
```

### 7. Scan with Custom Timing
```bash
nmap -T4 -sS -p- example.com
# Fast, aggressive SYN scan on all ports
```

### 8. Run Specific NSE Vulnerability Scripts
```bash
nmap --script vuln -sV example.com
# Identify known vulnerabilities in detected services
```

---

## Important Notes

⚠️ **Legal & Ethical Disclaimer**
- Only scan networks and systems you own or have explicit written permission to test
- Unauthorized network scanning may be illegal
- Use responsibly and ethically in authorized security assessments only

📝 **Best Practices**
- Run as root/administrator for accurate results
- Use `-Pn` for hosts behind firewalls that block ping
- Combine `-sV` with `-sC` for comprehensive assessments
- Use appropriate timing templates (`-T`) based on network conditions
- Document all scans with timestamps and purposes

🔧 **Troubleshooting**
- If no hosts found: Use `-Pn` to skip ping check
- Slow scans: Increase timing template (use `-T4` or `-T5`)
- Filtered ports: May indicate firewall; try different scan types
- Permission denied: Run as root/administrator

---

## Additional Resources

- **Official Manual**: `man nmap` or `nmap --help`
- **NSE Scripts Path**: `/usr/share/nmap/scripts/`
- **Documentation**: https://nmap.org/book/

