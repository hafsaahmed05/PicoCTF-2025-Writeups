# Guess my Cheese (Part 1) Challenge

## Challenge Description
```
Try to decrypt the secret cheese password to prove you're not the imposter!
Connect to the program on our server: nc verbal-sleep.picoctf.net 49370

Hint: Remember that cipher we devised together Squeexy? The one that incorporates your affinity for linear equations???
```

Challenge Link: https://play.picoctf.org/practice/challenge/473

## Solution
### 1. Understanding the Direct Substitution Cipher
A direct substitution cipher is one in which each letter of the plaintext is replaced with a corresponding letter from the cipher text.

### 2. Finding a Long Cheese Name from the Guess my Cheese (Part 2) Wordlist
From the wordlist provided in the challenge, we need to pick a long cheese name to work with. Use a cheese name that is lengthy enough to provide a variety of characters, as this will help in mapping encrypted letters to their correct plaintext letters.
I used  “Tasmania Highland Chevre Log” to decrypt. 
<img width="956" alt="image" src="https://github.com/user-attachments/assets/8d12bf5e-1e41-441a-ae56-933bd587824a" />

### 3. Use a direct substitution cipher given the encrypted cheese name to decrypt the given cheese name. 
Done manually. For unavailable letters or to fill in the gaps, reference the cheese list to complete.
![image](https://github.com/user-attachments/assets/e896dbbd-b419-47d1-9d4d-be92bf9265b8)
![image](https://github.com/user-attachments/assets/3fa1af13-4ccc-40da-b7c1-b49e2389958d)




