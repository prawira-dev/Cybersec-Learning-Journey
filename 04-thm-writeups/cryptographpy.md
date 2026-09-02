# Cryptography Basics

## Importance of Cryptography
Cryptography’s ultimate purpose is to ensure secure communication in the presence of adversaries.

Cryptography is used to protect confidentiality, integrity, and authenticity
Payment Card Industry Data Security Standard (PCI DSS).

https://www.pcisecuritystandards.org/documents/PCI_DSS_for_Large_Organizations_v1.pdf

## Plaintext to Ciphertext 
### **Sending proccess**
![Sender](../images/sender.svg)

### **Recive proccess**
![Recipient](../images/recipient.svg)

* **Plaintext** is the original, readable message or data before it’s encrypted. It can be a document, an image, a multimedia file, or any other binary data.
* **Ciphertext** is the scrambled, unreadable version of the message after encryption. Ideally, we cannot get any information about the original plaintext except its approximate size.
* **Cipher** is an algorithm or method to convert plaintext into ciphertext and back again. A cipher is usually developed by a mathematician.
* **Key** is a string of bits the cipher uses to encrypt or decrypt data. In general, the used cipher is public knowledge; however, the key must remain secret unless it is the public key in asymmetric encryption. We will visit asymmetric encryption in a later task.
* **Encryption** is the process of converting plaintext into ciphertext using a cipher and a key. Unlike the key, the choice of the cipher is disclosed.
* **Decryption** is the reverse process of encryption, converting ciphertext back into plaintext using a cipher and a key. Although the cipher would be public knowledge, recovering the plaintext without knowledge of the key should be impossible (infeasible).

### **Link for Encrypt and Decrypt**

https://cryptii.com/pipes/caesar-cipher

## Basic Math

### XOR
* If this is the first time you work with a truth table, it is a table that shows all possible outcomes. The XOR truth table above states all four cases: 0 ⊕ 0 = 0, 0 ⊕ 1 = 1, 1 ⊕ 0 = 1, and 1 ⊕ 1 = 0.

* Let’s consider an example where we want to apply XOR to the binary numbers 1010 and 1100. In this case, we perform the operation bit by bit: 1 ⊕ 1 = 0, 0 ⊕ 1 = 1, 1 ⊕ 0 = 1, and 0 ⊕ 0 = 0, resulting in 0110.


### MODULO
* 25%5 = 0 because 25 divided by 5 is 5, with a remainder of 0, i.e., 25 = 5 × 5 + 0
