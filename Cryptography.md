# Cryptography
- in cryptography, a *caesar cipher* is an ecnryption technique where a letter is replaced by another depending on a fixed number of positions through the alphabet
- can be represented by aligning two alphabets where the rotation can be any number of positions (up to person to decipher)

## Breaking a Cipher
1. an attacker knows or guesses the substitution cipher that has been used
2. an attacker knows that a Caesar cipher in is use, but does not know the shift value
    - can be solved by using brute force since there is a max number of shifts (25 in English)
        - done by writing out a snippet of the ciphertext in a table of all possible shifts
- polymorphism is when a cipher changes itself *for each time it is used!*
    - excellent way to add another layer of security

- asymmetric cryptography uses two different keys for encryption and decryption, as opposed to a single key used in symmetric cryptography
- key exchange algorithms are used to safely deliver info to unknown parties