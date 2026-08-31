# tcpdump Cheat Sheet

Command-line Interface (CLI) packet analyzer for network troubleshooting and security traffic inspection.

## Essential Commands & Flags

| Command / Flag | Function |
| :--- | :--- |
| `tcpdump -i eth0` | Capture traffic on a specific interface (`eth0`) |
| `tcpdump -n` | Do not resolve hostnames/IPs to DNS names (faster) |
| `tcpdump -nn` | Do not resolve IP addresses and resolve protocol numbers |
| `tcpdump -v` / `-vv` | Increase verbosity level (detailed packet headers) |
| `tcpdump -w capture.pcap` | Save captured packets to a PCAP file |
| `tcpdump -r capture.pcap` | Read and analyze a saved PCAP file |

## Practical Filtering Syntax

```bash
# Capture ICMP (ping) traffic only
tcpdump -i eth0 icmp

# Capture traffic from a specific source IP
tcpdump -i eth0 src 192.168.1.50

# Capture HTTP traffic (port 80)
tcpdump -i eth0 tcp port 80