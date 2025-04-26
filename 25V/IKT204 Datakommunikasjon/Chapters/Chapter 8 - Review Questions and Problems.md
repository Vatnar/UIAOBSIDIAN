**Exercise 1**

Explain Kerckhoff's principle with regard to cryptographic keys and encryption/decryption algorithms.


**Exercise 2**

What security property is provided by symmetric key and asymmetric key encryption?

**Exercise 3**

1. Consider symmetric key encryption. If an attacker gets hold of both a ciphertext and its underlying encrypted plaintext, can the attacker easily deduce the encryption key?
2. Consider asymmetric key encryption. If an attacker gets hold of both a ciphertext and its underlying encrypted plaintext, can the attacker easily deduce the private key?

**Exercise 4**

All block ciphers and certain public key encryption algorithms are deterministic, meaning that the same plaintext and key produces the same ciphertext.

1. Are block ciphers resistant to chosen plaintext attacks?
2. Are deterministic public key encryption algorithms resistant to chosen plaintext attacks?

**Exercise 5**

Checksums and CRC32 codes provide integrity protection concerning transmission errors.

1. Do hash functions provide integrity protection in this regard?
2. Do hash functions provide integrity protection regarding a (passive) eavesdropper?
3. Do hash functions provide integrity protection regarding an active adversary?

**Exercise 6**

Consider a hash function whose output length is 160 bits. Why is it difficult to find two different input messages that produce the same hash, i.e. h(m1)=h(m2)?

**Exercise 7**

What are the different purposes of link-layer MAC and cryptographic MAC?

**Exercise 8 (variant R15)**

After being victim of a fraudulent individual, Alice has decided to ensure the integrity of data she sends to her clients.

1. Would integrity protection make the clients confident that Alice is the originator and sender of her data?
2. Regarding protecting against fraudulent individuals, what is suitable of using 1) message digests, 2) MACs, or 3) digital signatures? Explain what is achieved by each alternative.

**Exercise 9 (variant R6)**

Suppose that a team of 10 persons are using symmetric key encryption to communicate securely with the other members of the team, without anybody else in the team being able to decrypt.

1. How many keys need to be shared in total among the team members?
2. Given the pairwise shared keys, how can four people in the group communicate securely together using symmetric key encryption (without anybody else in the team being able to decrypt).
3. Suppose that the group uses public key encryption instead. What is the answer to a) and b) in this case?

**Exercise 10**

What are the advantages of using public key encryption compared to secret key encryption? What potential security problem does public keys introduce, and how can this be mitigated?

**Exercise 11**

Why do digital signatures have a stronger security property (non-repudiation) compared to MACs (message authentication)?

**Exercise 12**

A digital certificate contains the name of the holder, a public key, and a digital signature.

1. Whose signature is it?
2. What is the purpose of digital signature certificates?
3. Does a single digital certificate guarantee this security goal?

**Exercise 13**

Replay attacks are a significant category of attacks.

1. What security property prevents replay attacks?
2. How can replay attacks be prevented?

**Exercise 14**

What is the difference between key transfer and key agreement? Why is key agreement preferable?

**Exercise 15 (R21)**

1. What is the purpose of the random nonces in the TLS handshake?
2. How do they achieve this purpose?