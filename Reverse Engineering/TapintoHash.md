# Tap into Hash

## Challenge Description
```
Description
Can you make sense of this source code file and write a function that will decode the given encrypted file content?
Find the encrypted file here. It might be good to analyze source file to get the flag.

Hints
1. Do you know what blockchains are? If so, you know that hashing is used in blockchains.
2. Download the encrypted flag file and the source file and reverse engineer the source file.
```

Challenge Link: https://play.picoctf.org/practice/challenge/466

Given files:
enc.flag
```
┌──(hahmed㉿kali)-[~/Downloads]
└─$ cat enc_flag 
Key: b'\x8b\x9a\x00G\xfe\xb3\xf3\x93\xdb\xa8yT\xfe\x15\x87a\xf4\xdf\x00\x8d\xee\xab\xd9\t^|\x04(%\x81\x9e\xf8'
Encrypted Blockchain: b'Z5Wo\xe9\xbd\xf4\xed<\xeb=\xcb%\xc4\xf0>S2\x0bl\xe9\xe9\xf0\xe8>\xe8n\x91q\xca\xad=\x01fRo\xbe\xba\xa2\xb5f\xb88\x90t\xc4\xaco\x041\x01n\xb3\xbd\xa1\xb4l\xee9\xc9u\x9e\xf1:O0\x035\xed\xeb\xf6\xean\xbei\xcc.\x9f\xfe8\x008\x04l\xef\xee\xf4\xe9g\xbf8\x9bt\x9f\xaanZ6\x0b8\xef\xbb\xa6\xb8>\xe9n\xcd$\xc5\xf08\x00eQ>\xef\xed\xf4\xeaf\xbdm\x9e \xcb\xfe9\x07-\x03=\xba\xb9\xa2\xbcl\xb4:\x9c&\x9e\xab8U4\x05=\xe8\xec\xa4\xeao\xefk\x9c#\x9a\xacn\x00bCd\xe8\xb7\xd6\xd8\x19\xf69\xc4x\x9f\xa2UQSae\xdd\xb1\xc7\xee\x0b\xbc*\xcbO\xa3\x91_\x08M\x03\x7f\xbf\xe1\xf6\xc4\x00\xfc\x18\xd2z\xb6\x93p Kl;\xbb\xee\xa1\xbb9\xef9\xd5t\x99\xf9;Ve\x04i\xb3\xe9\xf3\xbd;\xb8m\x91s\xcf\xff:\x019\x04=\xbd\xb9\xa4\xeff\xb5>\xcd:\xcc\xf9<Ta\x01?\xbd\xe9\xf0\xed=\xefi\x9fr\x98\xf8=[a\x00:\xbc\xba\xf3\xe9k\xeci\x90"\x98\xfbnZaPk\xed\xe9\xa6\xbf=\xe8>\x99.\xc5\xac?Wa\x02<\xbd\xb9\xa0\xeaj\xecn\x9b$\xd1\xf9:\x04dR:\xb9\xea\xa3\xedi\xebh\x9d\'\xcc\xfah\x008U9\xe8\xe8\xf6\xba>\xefk\x98#\xce\xfb;\x038\n?\xea\xb9\xf7\xbfg\xbbk\x90q\x9e\xacn[f\x06l\xef\xbb\xa7\xbaf\xbd9\x9a"\xcf\xcb\x08'
```

blockchain.py
```
┌──(hahmed㉿kali)-[~/Downloads]
└─$ cat block_chain.py
import time
import base64
import hashlib
import sys
import secrets


class Block:
    def __init__(self, index, previous_hash, timestamp, encoded_transactions, nonce):
        self.index = index
        self.previous_hash = previous_hash
        self.timestamp = timestamp
        self.encoded_transactions = encoded_transactions
        self.nonce = nonce

    def calculate_hash(self):
        block_string = f"{self.index}{self.previous_hash}{self.timestamp}{self.encoded_transactions}{self.nonce}"
        return hashlib.sha256(block_string.encode()).hexdigest()


def proof_of_work(previous_block, encoded_transactions):
    index = previous_block.index + 1
    timestamp = int(time.time())
    nonce = 0

    block = Block(index, previous_block.calculate_hash(),
                  timestamp, encoded_transactions, nonce)

    while not is_valid_proof(block):
        nonce += 1
        block.nonce = nonce

    return block


def is_valid_proof(block):
    guess_hash = block.calculate_hash()
    return guess_hash[:2] == "00"


def decode_transactions(encoded_transactions):
    return base64.b64decode(encoded_transactions).decode('utf-8')


def get_all_blocks(blockchain):
    return blockchain


def blockchain_to_string(blockchain):
    block_strings = [f"{block.calculate_hash()}" for block in blockchain]
    return '-'.join(block_strings)


def encrypt(plaintext, inner_txt, key):
    midpoint = len(plaintext) // 2

    first_part = plaintext[:midpoint]
    second_part = plaintext[midpoint:]
    modified_plaintext = first_part + inner_txt + second_part
    block_size = 16
    plaintext = pad(modified_plaintext, block_size)
    key_hash = hashlib.sha256(key).digest()

    ciphertext = b''

    for i in range(0, len(plaintext), block_size):
        block = plaintext[i:i + block_size]
        cipher_block = xor_bytes(block, key_hash)
        ciphertext += cipher_block

    return ciphertext


def pad(data, block_size):
    padding_length = block_size - len(data) % block_size
    padding = bytes([padding_length] * padding_length)
    return data.encode() + padding


def xor_bytes(a, b):
    return bytes(x ^ y for x, y in zip(a, b))


def generate_random_string(length):
    return secrets.token_hex(length // 2)


random_string = generate_random_string(64)


def main(token):
    key = bytes.fromhex(random_string)

    print("Key:", key)

    genesis_block = Block(0, "0", int(time.time()), "EncodedGenesisBlock", 0)
    blockchain = [genesis_block]

    for i in range(1, 5):
        encoded_transactions = base64.b64encode(
            f"Transaction_{i}".encode()).decode('utf-8')
        new_block = proof_of_work(blockchain[-1], encoded_transactions)
        blockchain.append(new_block)

    all_blocks = get_all_blocks(blockchain)

    blockchain_string = blockchain_to_string(all_blocks)
    encrypted_blockchain = encrypt(blockchain_string, token, key)

    print("Encrypted Blockchain:", encrypted_blockchain)


if __name__ == "__main__":
    text = sys.argv[1]
    main(text)
```

## Solution

Python script used to decrypt (from ChatGPT):
```
import base64
import hashlib

# Decrypt the ciphertext using the same XOR method
def xor_bytes(a, b):
    return bytes(x ^ y for x, y in zip(a, b))

def decrypt(encrypted_data, key):
    # Use the same block size as the encryption function (16 bytes)
    block_size = 16
    key_hash = hashlib.sha256(key).digest()

    # Decrypt the ciphertext
    decrypted_data = b''
    for i in range(0, len(encrypted_data), block_size):
        block = encrypted_data[i:i + block_size]
        decrypted_block = xor_bytes(block, key_hash)
        decrypted_data += decrypted_block

    # Remove padding
    padding_length = decrypted_data[-1]
    return decrypted_data[:-padding_length].decode('utf-8')

# Example usage:
key = b'\x8b\x9a\x00G\xfe\xb3\xf3\x93\xdb\xa8yT\xfe\x15\x87a\xf4\xdf\x00\x8d\xee\xab\xd9\t^|\x04(%\x81\x9e\xf8'
encrypted_blockchain = b'Z5Wo\xe9\xbd\xf4\xed<\xeb=\xcb%\xc4\xf0>S2\x0bl\xe9\xe9\xf0\xe8>\xe8n\x91q\xca\xad=\x01fRo\xbe\xba\xa2\xb5f\xb88\x90t\xc4\xaco\x041\x01n\xb3\xbd\xa1\xb4l\xee9\xc9u>

# Decrypting the Blockchain content
decrypted_blockchain = decrypt(encrypted_blockchain, key)
print("Decrypted Blockchain:", decrypted_blockchain)
```

![Screenshot 2025-03-16 181945](https://github.com/user-attachments/assets/d9207326-0f4d-415a-b0f9-e297f7dfe4e0)


