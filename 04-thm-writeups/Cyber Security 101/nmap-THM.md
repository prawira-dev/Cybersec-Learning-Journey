# Nmap: The Basics

## Host Discovery
```bash
nmap -sL 192.168.0.1/27
```
Machine will scan from 1 to 31

## Port Scanning: Who is Listening

```bash
sudo nmap -sS 10.49.177.125
```
Host is up (0.00016s latency).
Not shown: 994 closed tcp ports (reset)

| PORT | STATE | SERVICE |
|------|-------|---------|
| 7/tcp | open | echo |
| 9/tcp | open | discard |
| 13/tcp | open | daytime |
| 17/tcp | open | qotd |
| 22/tcp | open | ssh |
| 8008/tcp | open | http |

Nmap done: 1 IP address (1 host up) scanned in 0.13 seconds

## Version Detection
```bash
sudo nmap -sS -sV -d 10.49.177.125
```
need more time, please calm down to wait for the result.

| Port | State | Service | Reason | Version |
|-----|-----|---------|--------|-----------|
| 7/tcp | open | echo | syn-ack | ttl 64 |
| 9/tcp | open | discard? | syn-ack | ttl 64 |
| 13/tcp | open | daytime? | syn-ack | ttl 64 |
| 17/tcp | open | qotd? | syn-ack | ttl 64 |
| 22/tcp | open | ssh | syn-ack | OpenSSH 9.6p1 Ubuntu 3ubuntu13.5 (Ubuntu Linux; protocol 2.0) |
| 8008/tcp | open | http | syn-ack | lighttpd 1.4.74 |

## Timing
There are 5 timings
T0-T4