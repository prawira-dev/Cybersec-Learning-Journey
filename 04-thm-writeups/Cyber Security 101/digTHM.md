
I do ping first
```bash
ping -c 3 10.49.184.53
```
try to check what port is open
```bash
nmap -sS -sU -p 53 10.49.184.53
```

PORT   STATE  SERVICE
53/tcp closed domain
53/udp open   domain

port 53 UDP is open

so try to dig 
```bash
dig +notcp ANY givemetheflag.com @10.49.184.53
```

; <<>> DiG 9.18.39-0ubuntu0.24.04.5-Ubuntu <<>> +notcp ANY givemetheflag.com @10.49.184.53
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 64479
;; flags: qr aa; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;givemetheflag.com.		IN	ANY

;; ANSWER SECTION:
givemetheflag.com.	0	IN	TXT	**"FLAG IS HERE"**

;; Query time: 1 msec
;; SERVER: 10.49.184.53#53(10.49.184.53) (UDP)
;; WHEN: Mon Aug 31 16:57:18 UTC 2026
;; MSG SIZE  rcvd: 86
