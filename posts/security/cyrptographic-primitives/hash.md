---
layout: default
title: Hash
parent: Cryptographic Primitives
grand_parent: Security
---

A hash is a function that takes an input of arbitrary size and produces an output of fixed size (the output size being dependent on the hashing algorithm).

Hashing functions are used throughout web development. For example, passwords are often stored in the database as a [salted hash](/posts/index-of-terms/#salt).

## Hash Function Properties

Hashing functions have special properties that make them valuable for many cryptographic applications:

1. A given input always produces the same output.
2. It is computationally infeasible to determine a hash input given a hash output, i.e., it's a one-way function.
3. If the input of the hash function changes, the output also must change.
4. It is computationally infeasible to find two different hash inputs that hash to the same output (collision resistant).

## Common Hashing Algorithms

The most common hashing algorithms are in the [SHA family](https://en.wikipedia.org/wiki/Secure_Hash_Algorithms):

- SHA-256
- SHA-512

[MD5](https://en.wikipedia.org/wiki/MD5) was used in the past, but is now considered insecure due to producing collisions.

## Example

Let's take three separate SHA-256 hashes (you can do this on the command line via the `sha256sum` command).

```
knowweb.dev > echo -n 'Secret hash input' | sha256sum
bcdc609918b376066fe8c1e5edf30a8ddc2f02ba837cb16ba01c98d64ee1a65c
knowweb.dev > echo -n 'Secret hash input' | sha256sum
bcdc609918b376066fe8c1e5edf30a8ddc2f02ba837cb16ba01c98d64ee1a65c
knowweb.dev > echo -n 'A different input' | sha256sum
f6c493111b5f489bd7f4981ab35f5b1050d2d1ce5660018fa1c94fd8e1e02911
```

The first two are hashing the same input, `Secret hash input`, and produce the same hash output, `bcdc609918b376066fe8c1e5edf30a8ddc2f02ba837cb16ba01c98d64ee1a65c` (satisfying _Hash Property #1_ above). The third is a different input, `A different input`, and produces a completely different output (satisfying _Hash Property #3_ above).

Without knowing the input, if I were to ask you to compute the input given the SHA-256 hash value of `bcdc609918b376066fe8c1e5edf30a8ddc2f02ba837cb16ba01c98d64ee1a65c`, there would be no way to compute the input as "Secret hash input" (_Hash Property #2_). It would also be impossible to find a different input that produced the same hash output (#4).
