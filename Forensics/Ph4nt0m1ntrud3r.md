# Ph4nt0m 1ntrud3r Challenge

## Challenge Description
```
Description
A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag.
To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder!
Find the PCAP file here Network Traffic PCAP file and try to get the flag.

Hints:
1. Filter your packets to narrow down your search.
2. Attacks were done in timely manner.
3. Time is essential
```

Challenge Link: https://play.picoctf.org/practice/challenge/459

## Solution

### 1. Sort PCAP file based on the time the packages were sent.
![Screenshot 2025-03-16 133324](https://github.com/user-attachments/assets/0111ea70-0261-4444-b10b-ed170b358693)

### 2. Understand the attack.
Looking at the packages, it can be determined that the actual message started one packet before the message sent at time 0.0. This is determined based on the length of tha package which equals 12 for that packet and all of the following packets.

![Screenshot 2025-03-16 133533](https://github.com/user-attachments/assets/4c8048a3-094c-44a9-86fa-e3029958f540)

### 3. Then, copy the payload for all of the packets after that one.
All payloads:
```
cGljb0NURg==
ezF0X3c0cw==
bnRfdGg0dA==
XzM0c3lfdA==
YmhfNHJfZA==
MTA2NTM4NA==
fQ==
```
### 4. Use base64 decoder to decode payload
![Screenshot 2025-03-16 133702](https://github.com/user-attachments/assets/41dc4750-5441-4508-aa5d-4d2705793012)




