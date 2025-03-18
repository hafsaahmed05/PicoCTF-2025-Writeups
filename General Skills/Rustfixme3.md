# Rust fixme 3 Challenge

## Challenge Description
```
Description
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!
Download the Rust code here.

Hints:
1. Read the comments...darn it!
```

Challenge Link: https://play.picoctf.org/practice/challenge/463

## Solution

Given file:
```
use xor_cryptor::XORCryptor;

fn decrypt(encrypted_buffer: Vec<u8>, borrowed_string: &mut String) {
    // Key for decryption
    let key = String::from("CSUCKS");

    // Editing our borrowed value
    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");

    // Create decryption object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        return;
    }
    let xrc = res.unwrap();

    // Did you know you have to do "unsafe operations in Rust?
    // https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html
    // Even though we have these memory safe languages, sometimes we need to do things outside of the rules
    // This is where unsafe rust comes in, something that is important to know about in order to keep things in perspective
    
    // unsafe {
        // Decrypt the flag operations 
        let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);

        // Creating a pointer 
        let decrypted_ptr = decrypted_buffer.as_ptr();
        let decrypted_len = decrypted_buffer.len();
        
        // Unsafe operation: calling an unsafe function that dereferences a raw pointer
        let decrypted_slice = std::slice::from_raw_parts(decrypted_ptr, decrypted_len);

        borrowed_string.push_str(&String::from_utf8_lossy(decrypted_slice));
    // }
    println!("{}", borrowed_string);
}

fn main() {
    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "12", "90", "7e", "53", "63", "e1", "01", "35", "7e", "59", "60", "f6", "03", "86", "7f", "56", "41", "29", "30", "6f", "08", "c3", "61", "f9", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    let mut party_foul = String::from("Using memory unsafe languages is a: ");
    decrypt(encrypted_buffer, &mut party_foul);
}
```

### 1. Make sure you have RUST environment set-up on Visual Studio.
Instructions: https://learn.microsoft.com/en-us/windows/dev-environment/rust/setup

### 2. Unsafe function error.
Fixed using chatGPT

![Screenshot 2025-03-13 122224](https://github.com/user-attachments/assets/a5454ae4-1821-4df6-9268-c7efa25995ac)

### 3. Update code and run file. 

Updated Function
```
fn decrypt(encrypted_buffer: Vec<u8>, borrowed_string: &mut String) {
    let key = String::from("CSUCKS");

    borrowed_string.push_str("PARTY FOUL! Here is your flag: ");

    let res = XORCryptor::new(&key);
    if res.is_err() {
        return;
    }
    let xrc = res.unwrap();

    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);

    let decrypted_ptr = decrypted_buffer.as_ptr();
    let decrypted_len = decrypted_buffer.len();

    // ** Fix: Wrap the unsafe function call in an `unsafe` block **
    let decrypted_slice = unsafe {
        std::slice::from_raw_parts(decrypted_ptr, decrypted_len)
    };

    borrowed_string.push_str(&String::from_utf8_lossy(decrypted_slice));

    println!("{}", borrowed_string);
}
```

![Screenshot 2025-03-13 122325](https://github.com/user-attachments/assets/855c9f87-e5ec-4387-a4ad-d0829d99e91c)



