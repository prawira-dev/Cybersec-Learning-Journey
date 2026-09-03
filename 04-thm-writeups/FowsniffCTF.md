# Fowsniff

* Start the machine and attacker
scan using 
```bash
nmap -A -p- -sV MACHINE_IP
```
* **Key Flag:**
    * `nmap`: Launches the Network Mapper tool
    * `-A`: Agresive scan
    * `-p-`: Scan all TCP port
    * `-sV`: Service Version
    * `MACHINE_IP`: target IP, hostname or web address

------

* Check what port are open, it should be:
    * port 22/tcp - SSH - (OpenSSH 7.2p2)
    * port 80/tcp - HTTP - (Apache httpd 2.4.18)
    * port 110/tcp - POP3 - (Dovecot pop3d)
    * port 143/tcp - IMAP - (Dovecot imapd)

* If you search using google you will found that Fowsniff Corp have breached, attacker hijack the  [@fowsniffcorp](https://x.com/fowsniffcorp) Twitter account and dumped employee usernames and hashed passwords on Pastebin but you can't access it anymore so use this github link (it will show on top when you google it)

https://github.com/berzerk0/Fowsniff

* There will be user and password for the email.
you can use but the password still md5 hash
I use this website to Decrypt
https://md5decrypt.net/en/

```bash
nc <TARGET_IP> 110
```
* **Key Flag:**
    * `nc`: launch netcat you can just use `netcat` too
    * `TARGET_IP` : target IP, hostname or web address
    * `110` : port for POP3
---
* Once connected, use the `RETR` command to read her emails. You will found the temporary password set for her.

