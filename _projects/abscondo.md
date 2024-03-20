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

### The Secret Handshake: *Diffie-Hellman Key Exchange* ###
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