# FILE ENCRYPTER POWERED BY OPENSSL

**DISCLAIMER: THIS WAS MADE FOR TEST PURPOSE SO DON'T USE THIS SCRIPT FOR ENCRYPTION OF SENSITIVE FILE**

Encrypts/Decrypts the file with AES-256 (for the file) and RSA (for the key).

Available commands:

**Encryption**

```
file-encrypter enc <rsa_public_key> <input_file>
    Encrypts the input file. The output file name should be '<input_file>.enc'.
    and <rsa_public_key> must be a more 1024 bit of PKCS8 format.
```

1. Generate the 256-bit-random key which is used to encrypt the file with AES-256 cipher
2. Encrypt `<input_file>` by AES-256-CBC cipher with the key generated before
3. Encrypt the AES key by RSA with `<rsa_public_key>`  
4. Combine both of 2 and 3 that we encoded into Base64 in advance

**Decryption**

```
file-encrypter dec <rsa_private_key> <input_file>
    Decrypts the input file. The output file name should be dropped '.enc' extension from '<input_file>' (i.e. The original file name before your encryption).
```

1. Split `<input_file>` into encrypted AES random key and encrypted body
2. Decrypt the AES random key by AES-256-CBC `<rsa_private_key>`
3. Decrypt the encrypted body by RSA with the key decrypted before
