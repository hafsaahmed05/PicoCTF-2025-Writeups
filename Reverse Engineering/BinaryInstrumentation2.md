# Binary Instrumentation 2 Challenge

## Challenge Description
```
Description
I've been learning more Windows API functions to do my bidding. Hmm... I swear this program was supposed to create a file and write the flag directly to the file. Can you try and intercept the file writing function to see what went wrong?
Download the exe here. Unzip the archive with the password picoctf

Hints:
1. Frida is an easy-to-install, lightweight binary instrumentation toolkit
2. Try using the CLI tools like frida-trace to auto-generate handlers
3. You can specify the exact function name you want to trace
```

Challenge Link: https://play.picoctf.org/practice/challenge/452

## Solution
Source: https://www.youtube.com/@ItsMeChaste

### 1. Use binwalk on .exe file: 
```
binwalk -e  bininst2.exe
```
![Screenshot 2025-03-16 233716](https://github.com/user-attachments/assets/b61976fd-c94a-421d-8db3-cfb163609d07)

### 2. Running the command will give the following compressed data
![image](https://github.com/user-attachments/assets/2b0a68c7-7f1c-433c-a645-5974175a2233)

### 3. Run strings function on the 6000 file in the compressed data
```
strings 6000
```
![image](https://github.com/user-attachments/assets/0534dac5-9496-4d0e-8210-804a812ea0ad)

### 4. Base64 Decode
![Screenshot 2025-03-16 234150](https://github.com/user-attachments/assets/022a8751-41fa-43fa-b19d-05fd15ac42e5)


