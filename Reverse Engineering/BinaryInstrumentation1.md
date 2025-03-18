# Binary Instrumentation 1 Challenge

## Challenge Description
```
Description
I have been learning to use the Windows API to do cool stuff! Can you wake up my program to get the flag?
Download the exe here. Unzip the archive with the password picoctf

Hints:
1. Frida is an easy-to-install, lightweight binary instrumentation toolkit
2. Try using the CLI tools like frida-trace to auto-generate handlers
```

Challenge Link: https://play.picoctf.org/practice/challenge/451

## Solution
Source: https://www.youtube.com/@ItsMeChaste
### 1. Use binwalk on .exe file: 
```
binwalk -e  bininst1.exe
```
![Screenshot 2025-03-16 233716](https://github.com/user-attachments/assets/b61976fd-c94a-421d-8db3-cfb163609d07)

### 2. Running the command will give the following compressed data
![Screenshot 2025-03-16 233740](https://github.com/user-attachments/assets/db8cb18e-29dc-46e9-9d0b-802d9ec84b73)

### 3. Run strings function on the 6000 file in the compressed data
```
strings 6000
```
![Screenshot 2025-03-16 233810](https://github.com/user-attachments/assets/73555b63-f416-48e3-b0d8-50b0c95e4494)
### 4. Base64 Decode
![Screenshot 2025-03-16 233823](https://github.com/user-attachments/assets/44055203-a6f4-47e4-8ec2-0cde58c4a665)

