# PIE TIME Challenge

## Challenge Description
```
Description
A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server?
Access the server using nc verbal-sleep.picoctf.net 57271

Hints:
1. Understanding hashes is very crucial. Read more here.
2. Can you identify the hash algorithm? Look carefully at the length and structure of each hash identified.
3. Tried using any hash cracking tools?
```

Challenge Link: https://play.picoctf.org/practice/challenge/475

## Solution

### 1. Connect to server using given command.
### 2. Use hashcat and rockyou.txt to do a dictionary attack and retrieve password

Identify hash type using https://hashes.com/en/tools/hash_identifier

Use the following commands:
For md5 - 
```
hashcat -m 0 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt
```
For sha1
```
hashcat -m 100 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt
```
For sha256
```
hashcat -m 1400 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt
```

![Screenshot 2025-03-13 121012](https://github.com/user-attachments/assets/e769ea17-f1a6-44d3-a7c1-84f1e31375f7)



