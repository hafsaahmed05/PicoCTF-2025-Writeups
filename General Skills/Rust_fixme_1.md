# Rust fixme 1 Challenge

## Challenge Description
```
Description
Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!
Download the Rust code here.

Hints:
1. Cargo is Rust's package manager and will make your life easier. See the getting started page here
2. println!
3. Rust has some pretty great compiler error messages. Read them maybe?
```

Challenge Link: https://play.picoctf.org/practice/challenge/461

## Solution

Given file:
```
use xor_cryptor::XORCryptor;

fn main() {
    // Key for decryption
    let key = String::from("CSUCKS") // How do we end statements in Rust?

    // Encrypted flag values
    let hex_values = ["41", "30", "20", "63", "4a", "45", "54", "76", "01", "1c", "7e", "59", "63", "e1", "61", "25", "7f", "5a", "60", "50", "11", "38", "1f", "3a", "60", "e9", "62", "20", "0c", "e6", "50", "d3", "35"];

    // Convert the hexadecimal strings to bytes and collect them into a vector
    let encrypted_buffer: Vec<u8> = hex_values.iter()
        .map(|&hex| u8::from_str_radix(hex, 16).unwrap())
        .collect();

    // Create decrpytion object
    let res = XORCryptor::new(&key);
    if res.is_err() {
        ret; // How do we return in rust?
    }
    let xrc = res.unwrap();

    // Decrypt flag and print it out
    let decrypted_buffer = xrc.decrypt_vec(encrypted_buffer);
    println!(
        ":?", // How do we print out a variable in the println function? 
        String::from_utf8_lossy(&decrypted_buffer)
    );
}
```

### 1. Make sure you have RUST environment set-up on Visual Studio.
Instructions: https://learn.microsoft.com/en-us/windows/dev-environment/rust/setup

### 2. Run code with "cargo run" command. 

#### Detects 3 syntax errors:

1.  No semicolon at the end
```
let key = String::from("CSUCKS") 
```
Fixed
```
let key = String::from("CSUCKS");
```
2. Change ret to return
```
if res.is_err() {
    ret; // How do we return in rust?
}
```

Fixed
```
if res.is_err() {
    return; // How do we return in rust?
}
```

3. 
Incorrect way to print
From this -
```
println!(
    ":?", // How do we print out a variable in the println function? 
    String::from_utf8_lossy(&decrypted_buffer)
);
```

Fixed -
```
println!("{}", String::from_utf8_lossy(&decrypted_buffer));
```

#### After Fix
![Screenshot 2025-03-13 124223](https://github.com/user-attachments/assets/d57a7e82-06e0-4444-975b-40d289950056)


