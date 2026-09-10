# **Tcpdump: The Basics**
## Basic Packet Capture
### Captures and displays 50 packets (eth0) displays them verbosely.
```bash
tcpdump -i eth0 -c 50 -v 
```
* **Key Flags**:
    * -i ```eth0``` : Focuses capture exclusively on the ```eth0``` network interface.
    * -c ```50``` : Limits the capture to exactly 50 packets, then automatically stops execution.
    * -v : Enables verbose output (shows TTL, identification, flags, length, and options).

### Capture packets from all interfaces
```bash
tcpdump -i any -nn
```
* **Key Flags**:
    * -i ```any``` : Captures traffic across all active network interfaces simultaneously.
    * -nn : Disables DNS host resolution AND port name lookup (shows raw IP addresses and numeric port numbers for faster performance).

## Filtering
### Count Specific Packets in PCAP File

```bash
tcpdump -r traffic.pcap icmp -n | wc -l
```
* **Purpose**: Counts the total number of ICMP (ping) packets stored inside a PCAP file.

* **Key Flags**:
    * -r ```<traffic.pcap>``` : Reads from a saved PCAP file.
    * icmp : Filters traffic to show only ICMP packets.
    * -n : Prevents IP-to-hostname resolution for faster execution.
    * | wc -l : Pipes the output into Word Count to calculate the total line count (1 line = 1 packet).

* **Use Case**: Useful during network forensics or log analysis to quickly determine the volume of ping sweeps or ICMP flood activity without scrolling through raw packet output.

## Analyze ARP Traffic in PCAP File

```bash
sudo tcpdump -r traffic.pcap arp -n
```
* **Purpose**: Reads a PCAP file and filters it to display only ARP (Address Resolution Protocol) packets without resolving IP addresses to hostnames.

* **Key Flags**:
    * sudo : Runs tcpdump with root privileges (often required to access packet captures or raw network sockets).
    * -r ```<traffic.pcap>``` : Reads packets from the specified PCAP file instead of capturing live traffic.
    * arp : Protocol filter that isolates ARP traffic (IP-to-MAC address mapping requests and replies).
    * -n : Disables DNS name resolution to keep output fast and show raw IP addresses.
* **Use Case**: Useful during network forensics or troubleshooting to detect ARP spoofing/poisoning attacks, IP conflict issues, or host discovery activity on a local network.

## Analyze ARP Traffic in PCAP File

```bash
sudo tcpdump -r traffic.pcap arp -n
```
* **Purpose**: Reads a PCAP file and filters it to display only ARP (Address Resolution Protocol) packets without resolving IP addresses to hostnames.
* **Key Flags**:
    * sudo : Runs tcpdump with root privileges (often required to access packet captures or raw network sockets).
    * -r traffic.pcap : Reads packets from the specified PCAP file instead of capturing live traffic.
    * arp : Protocol filter that isolates ARP traffic (IP-to-MAC address mapping requests and replies).
    * -n : Disables DNS name resolution to keep output fast and show raw IP addresses.
* **Use Case**: Useful during network forensics or troubleshooting to detect ARP spoofing/poisoning attacks, IP conflict issues, or host discovery activity on a local network.

## Advance Filtering
### Count TCP Reset (RST) Packets in PCAP File

```bash
tcpdump -r traffic.pcap "tcp[tcpflags] == tcp-rst" -n | wc -l
```
* **Purpose:** Reads a PCAP file, isolates TCP packets that have the RST (Reset) flag explicitly set, and counts the total number of these packets.

* **Key Flags:**
    * -r traffic.pcap : Reads packets from a saved PCAP file.
    * "tcp[tcpflags] == tcp-rst" : Advanced BPF (Berkeley Packet Filter) primitive that matches packets where the TCP header RST flag is enabled.
    * -n : Disables IP-to-hostname DNS resolution for faster analysis.
    * | wc -l : Pipes the output into Word Count to return the total line count (1 packet = 1 line).
* **Use Case:** Essential during incident response and network security audits to measure connection rejection rates, detect stealth SYN/Xmas port scans (where closed ports send RST packets back), or identify active TCP connection teardowns caused by inline security appliances (like IPS or Firewalls).

### Filter Large Packets (>15,000 Bytes) in PCAP File

```bash
tcpdump -r traffic.pcap 'greater 15000' -n
```
* **Purpose:** Reads a PCAP file and filters it to display only oversized packets whose total length (payload plus headers) is greater than 15,000 bytes, without resolving IP addresses to hostnames.
* **Key Flags:**
    * -r traffic.pcap : Reads input packets from a saved PCAP file.
    * 'greater ```<length>```' : Filters packets that have a length greater than or equal to the specified length
    * -n : Disables DNS host resolution to speed up output and display raw numeric IP addresses.
* **Use Case:** Crucial during network forensics and anomaly detection to identify large file transfers, data exfiltration attempts over non-standard channels, IP fragmentation issues, or abnormal Jumbo Frame traffic across network interfaces.

### Inspect ARP Packets with Data Link (MAC) Headers

```bash
tcpdump -r traffic.pcap arp -e -n -c 5
```
* **Purpose:** Reads a PCAP file and displays the first 5 ARP packets along with their link-level (Ethernet/MAC address) headers, without resolving IP addresses to hostnames.
* **Key Flags:**
    * -r ```traffic.pcap``` : Reads input packets from a saved PCAP file.
    * arp : Filters output to include only ARP (Address Resolution Protocol) traffic.
    * -e : Prints the link-level header on each dump line (displays source and destination MAC addresses).
    * -n : Disables DNS name resolution to keep output fast and show numeric IP addresses.
    * -c 5 : Limits execution to process and output exactly 5 matching packets.
* **Use Case:** Critical during network forensics to investigate Layer 2 threats such as ARP spoofing, Man-in-the-Middle (MITM) attacks, or MAC address impersonation by cross-referencing IP-to-MAC mappings directly from the Ethernet frame headers.
