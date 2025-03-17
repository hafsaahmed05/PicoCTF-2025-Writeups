# EVEN RSA CAN BE BROKEN??? Challenge

## Challenge Description
```
This service provides you an encrypted flag. Can you decrypt it with just N & e?
Connect to the program with netcat:
$ nc verbal-sleep.picoctf.net 55822
The program's source code can be downloaded here.

Hint:
1. How much do we trust randomness?
2. Notice anything interesting about N?
3. Try comparing N across multiple requests
```

Challenge Link: https://play.picoctf.org/practice/challenge/470

## Solution
### 1. Connect to server to retreive given values.
### 2. Get factor of given N from factordb.com 
![Screenshot 2025-03-16 151852](https://github.com/user-attachments/assets/e9c89aff-b08a-4646-8b97-7dbc6265396b)

### 3. Python script to compute d and q and then decrypt the message
```
# Given values
N = 20953571113283575572259664553223424962754454537663690108589791893632504038809588381801826908039399667459730525363264483377065329790347911704702727064711054
p = 10476785556641787786129832276611712481377227268831845054294895946816252019404794190900913454019699833729865262681632241688532664895173955852351363532355527
e = 65537
ciphertext = 8205417759734714833704637470173257893072176625745581600977409590877310753421296408677153813945934797061455032468221706582870153199115807873242651098128869

# Step 1: Calculate q
q = N // p

# Step 2: Calculate (p-1)*(q-1)
phi_N = (p - 1) * (q - 1)

# Step 3: Calculate d (the private exponent)
# Modular inverse of e mod phi(N)
d = pow(e, -1, phi_N)

# Step 4: Decrypt the ciphertext
# Decrypt using RSA: m = ciphertext^d % N
plaintext = pow(ciphertext, d, N)

# Convert the decrypted number back to bytes
# Assuming the decrypted number is the flag (as a long integer)
flag = long_to_bytes(plaintext).decode('utf-8')

# Output the result
print("Decrypted Flag:", flag)
```
### 4. Run the program and get the flag.
![Screenshot 2025-03-16 152646](https://github.com/user-attachments/assets/0cf4eeec-fa7c-4e50-a49f-a2e384df0c69)

