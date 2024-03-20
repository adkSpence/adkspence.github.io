---
layout: post
title: ABSCONDO - Journal App
description: Abscondo is a journalling app I built where users can encrypt and decrypt information
---

A Hybrid Cryptographic System based on Diffie-Hellman Key Exchange and Triple DES Algorithms

Table of Content:
---

  * [Demo](#demo)
  * [Introduction](#introduction)
  * [Overview of Algorithms](#overview-of-algorithms-sharing-secrets-and-keeping-messages-safe)
  * System Architecture
  * Future Work
  * Conclusion

DEMO
---

<iframe class="video" src="https://www.dropbox.com/scl/fi/47b5wxwl444zgyn6124cn/demo.mp4?rlkey=cw8ngjb2teikgk4vrcx2kp7q0&raw=1" width="640" height="480" allowfullscreen frameborder="0"></iframe>


***

INTRODUCTION
---
> In the world of information security, the mathematician holds the key. The essence of cryptography is less about hiding information from prying eyes and more about the art of ensuring that the eyes meant to see it can do so unimpeded.

`Okay, before we dive in, let's address the elephant in the room: "Abscondo"? Yes!!! In Latin, "Abscondo" means to hide, conceal, cover, or shroud. It comes from the Latin words "abs-" meaning "from, away from" and "condō" meaning "to conceal, hide". Why did we fall in love with the name? Well, who would't? 😏`

In the digital age, where data traverses the globe in the blink of an eye, the sanctity of information has never been more paramount. As we exchange bytes over the vast, open wilderness of the Internet, the invisible threads that secure these exchanges become the lifelines of our privacy and security. Enter the realm of cryptography: a discipline as ancient as it is pivotal in our modern world, evolving continuously to protect our most precious asset—information.

This blog post delves into the intricate dance of cryptographic algorithms. At the heart of our discussion is a hybrid system, ingeniously marrying the Diffie-Hellman Key Exchange with Triple DES encryption.

Join me and my esteemed colleague, Pimpa Akuffo Sophia, as we delve into the intricacies of this cryptographic duet, the cornerstone of our final year undergraduate project. Our endeavor simulates a secure journal application, demonstrating the practical application of the hybrid combination of both algorithms within a single, unified platform. This simulation not only showcases the robustness of combining asymmetric and symmetric encryption methods but also illustrates how such a hybrid system can be ingeniously applied to everyday digital tools like a personal journal app.

**This simulation ensures that even if unauthorized access to one's password or a direct attack on the database were to occur, the stored information would remain an unintelligible jumble of characters, safeguarded by the robust encryption of Triple DES.**

OVERVIEW OF ALGORITHMS: Sharing Secrets and Keeping Messages Safe
---
Imagine you have a secret clubhouse, and you want to send secret messages to your friend. But, oh no! You have to make sure no one else can read them. How do you do it? Well, it's a bit like sharing a secret handshake, and we have two special ways to keep our club's messages super-secret.

### **The Secret Handshake:** *Diffie-Hellman Key Exchange* ###
The first algorithm we discuss is called Diffie-Hellman Key Exchange. It's like creating a secret handshake, but even if someone sees you doing it, they still can't guess the secret! It's a clever trick where you and your friend both pick a special number, mix it with your club's secret number, and then swap the results. But here's the magical part: you both end up with the `same secret number` at the end without ever having to whisper it directly to each other. This algorithm falls under the category of `asymmetric encryption algorithms`. What this means is that: one key to encrypt the data (the public key) and another key to decrypt it (the private key). These keys are mathematically linked—whatever is encrypted with the public key can only be decrypted with the corresponding private key, and vice versa. In the case of our Secret Clubhouse analogy, one is a public key that everyone can see (like waving hello), and the other is a private key that only you know (like the secret handshake itself).

### Simplified Pseudocode ###
~~~
1. Choose two prime numbers:
   - p (a large prime number)
   - g (a primitive root modulo p, also known as a generator)

   2. Alice generates her private key:
      - a (Alice's private key, chosen randomly)

   3. Bob generates his private key:
      - b (Bob's private key, chosen randomly)

   4. Alice calculates her public key:
      - A = g^a mod p
      (Alice raises g to the power of a and then takes the modulo p of the result to get her public key A)

   5. Bob calculates his public key:
      - B = g^b mod p
      (Bob raises g to the power of b and then takes the modulo p of the result to get his public key B)

   6. Alice and Bob exchange their public keys (A and B) over an insecure channel.

   7. Alice computes the shared secret using Bob's public key:
      - s = B^a mod p
      (Alice raises Bob's public key B to the power of her private key a and takes the modulo p of the result to get the shared secret s)

   8. Bob computes the shared secret using Alice's public key:
      - s = A^b mod p
      (Bob raises Alice's public key A to the power of his private key b and takes the modulo p of the result to get the shared secret s)
~~~
At this point, both Alice and Bob have computed the same shared secret s, which can be used as a key for further symmetric encryption. The security of Diffie-Hellman Key Exchange lies in the difficulty of the Discrete Logarithm Problem, making it computationally infeasible for an eavesdropper to derive the shared secret without knowing the private keys.

### **The Secret Box:** *Triple DES* ###
Now, the second method is called Triple DES. Think of it as a secret box with a lock. When you put a message inside and turn the key three times, it gets locked up so tight that only your friend with the correct key can open it and read the message. This is called "symmetric" because you and your friend use the same secret key to lock and unlock the box. More formally, Triple DES (3DES) is a symmetric-key encryption algorithm that applies the Data Encryption Standard (DES) cipher algorithm three times to each data block. The simplified pseudocode for encrypting and decrypting with Triple DES is as follows:

### Simplified Pseudocode: Encryption ###
~~~
1. Input:
   - plaintext: The data you want to encrypt.
   - key1, key2, key3: Three DES keys, each typically 56 bits long.

2. Procedure:
   - Encrypt the plaintext using key1 (DES encryption).
     encrypted1 = DES_Encrypt(plaintext, key1)

   - Decrypt the result from step 1 using key2 (DES decryption, acting as a second layer of encryption).
     encrypted2 = DES_Decrypt(encrypted1, key2)

   - Encrypt the result from step 2 using key3 (DES encryption, third layer).
     ciphertext = DES_Encrypt(encrypted2, key3)

3. Output:
   - ciphertext: The encrypted data, after applying Triple DES.
~~~

### Simplified Pseudocode: Decryption ###
~~~
1. Input:
   - ciphertext: The data you want to decrypt, which was encrypted with Triple DES.
   - key1, key2, key3: The same three keys used for encryption.

2. Procedure:
   - Decrypt the ciphertext using key3 (DES decryption, reversing the third encryption layer).
     decrypted1 = DES_Decrypt(ciphertext, key3)

   - Encrypt the result from step 1 using key2 (DES encryption, reversing the second layer, which was originally decryption).
     decrypted2 = DES_Encrypt(decrypted1, key2)

   - Decrypt the result from step 2 using key1 (DES decryption, reversing the first encryption layer).
     plaintext = DES_Decrypt(decrypted2, key1)

3. Output:
   - plaintext: The original data, after reversing the Triple DES encryption.
~~~
NB: This pseudocode abstracts away the details of the DES algorithm and assumes the existence of DES_Encrypt and DES_Decrypt functions which perform DES encryption and decryption respectively. It also doesn't address padding, mode of operation, or initialization vectors (IVs) which are important for real-world implementations.

### **Working Together** ###
So, how do we use these two methods for our clubhouse? First, we do our secret handshake using Diffie-Hellman to create a secret key that only you and your friend know. Then, you use that key to lock your message in the Triple DES secret box. Now, you can send your secret message across the playground, and even if someone else finds it, they can't open the box and read it!

It's like having an invisible cloak for your messages, making sure they stay just between you and your friend, safe and sound. And that's how our clubhouse keeps its secrets super-secret!

In our journal app, the Diffie-Hellman Key Exchange is used conceptually to illustrate how a shared secret key can be generated in a secure manner. This shared secret is then utilized within your app as the symmetric key for Triple DES encryption, ensuring that journal entries are encrypted and can only be decrypted by someone with access to the secret key.