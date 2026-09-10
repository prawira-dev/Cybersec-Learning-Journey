# John The Ripper Basic

## Setting Up System
Just click start the attacker machine and lab

## Cracking basic hash
```
wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py
```
to get hash-id.py to the attacker terminal

### **Format-Specific Cracking**

john --format=[format] --wordlist=[path to wordlist] [path to file]

Example Usage:
```
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```
there will be 3 hash to check in task 4 folder

## Cracking Password Protected Zip and Rar File
### Unzip using Zip2John
```
zip2john [options] [zip file] > [output file]
```
* **Key Flag**
    * `[options]`: Allows you to pass specific checksum options to zip2john; this shouldn’t often be necessary
    * `[zip file]` : The path to the Zip file you wish to get the hash of
    * `>` : This redirects the output from this command to another file
    * `[output file]`: This is the file that will store the output

**Example Usage**
```
zip2john zipfile.zip > zip_hash.txt
```

### Cracking
```
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```
* **Key Flag**
    * john
    * --wordlist=
    * /usr/share/wordlists/rockyou.txt
    * zip_hash.txt

```
unzip -P PASSWORD secure.zip
```
* **Key Flag**
    * unzip
    * -P
    * secure.zip

For rar use the same patern
```
rar2john secure.rar > rar_hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
unrar x secure.rar
```
Except 
```
unrar x -p- secure.rar
```

## Cracking SSH Keys using John
```
ssh2john [id_rsa private key file] > [output file]
```
* **Key Flag**
    * `ssh2john`: Invokes the ssh2john tool
    * `[id_rsa private key file]`: The path to the id_rsa file you wish to get the hash of
    * `>`: This is the output director. We’re using it to redirect the output from this command to another file.
    * `[output file]`: This is the file that will store the output from

Example Usage
```
/opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
```
