# Encryption_101

- encryption at rest 
- encryption in transit
- concepts
  - plaintext - its un-encrypted data, like text file, images, images or applications
    - its a data that you can load into application and use or immidiately read it
  - Algorithm 
    - piece of code or maths, which takes plaintext and an encryption key to generate encrypted data
    - example of algo, Blowfish, AES, RC4, DES, RC5, RC6
  - Key
    - its like a password, something which should be very secure 
  - Ciphertext
    - the output of algorithm is ciphertext, which was used by giving input like key and plaintext
    - its not always text data, its an encrypted data

### Types of Key

- Symmetric encryption
  - Symmetric key is used in this encryption technique
  - same key needs to be used for encryption and decryption
  - it is mostly used to encrypt data at rest, because key can't be transferred over internet/network
  - its good for, local file encryption or disc encryption on laptops.
  
- Asymmetric encryption
  - it formed of 2 parts (public key and private key)
  - both parties needs to agree on one encryption algorithm
  - public key can be used to encrypt the data
  - but only private key can be used to decrypt the data
  - hence, only one party who is receiving the data should generate the public/private key-pair
  - used by popular email and file encryption systems, SSL, TLS, which is a system for encrypting browser communications,
  - ssh also used the same method, to securely access servers
  - encryption doesn't prove identity


### key points to understand while working with Asymmetric encryption
### Signing
- Its a way of making sure, the two patries can identify each and make and make sure they are communicating with the right party.
- signing a doc can be done using private key. this is just to prove that its coming from correct party.

### Steganography
- its a method of hiding something in something else
- for example, a file can be encrypted and then hide inside some other file. Although, the new file is very similar to original, but only the known parties can understand the difference.
