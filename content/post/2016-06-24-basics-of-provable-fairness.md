---
author: Alex Vanderpot
categories:
- Uncategorized
date: "2016-06-24T04:16:54Z"
guid: https://vanderpot.com/?p=78
id: 78
title: Basics of Provable Fairness
url: /2016/06/basics-of-provable-fairness/
---

This post is a basic primer on how provably fair betting websites and number generation algorithms work. It contains helpful background information for some of my future posts.

# Words to Know

Provably fair number generation algorithms are built around cryptographic hashes. Provably fair systems rely on these hash functions taking input data (the **plaintext** or **message**) and outputting a representation of that data that can not be reversed, but is the same every time (the **hash** or **message digest**). These hash functions can be broken by brute force if the plaintext is is short enough. Therefore, in order for a hash to be secure, the plaintext must be long enough and complex enough so that the hash can not be broken by brute force.

Two other terms that are commonly used in describing a provably fair number generation algorithm are the **server** and the **client**. The **server** is the digital equivalent of the “house” or casino. The **client** is the gambler or you.

# Most Provably Fair Algorithms

Most provably fair number generation algorithms work similarly to the steps below.

1. The server generates a **server seed**. The server seed is usually a random string of numbers and letters that is long enough to be considered cryptographically secure.
2. The server **hashes** the server seed and sends it to the client. The client saves this information so that the round can be verified later.
3. The client generates a **client seed** and sends it to the server. This is another string of numbers and letters. However, this string does not have to be cryptographically secure because it is never used in an important hash function.
4. The server concatenates the plaintext of the server seed, the client seed, and a counter value. The server converts this value into a number and uses that as the roll result.
5. The server increments the counter value and repeats step 4 for each subsequent roll. The client seed is also regenerated.
6. When the game is over, the server sends the plaintext of the server seed to the client.

# Why does this work?

This algorithm guarantees that neither the client nor server can influence the results of the numbers generated. Because the client knows the hash of the server seed before the roll, the client can verify that the server seed was not changed during the game. Therefore, the client can verify all of the inputs to the number generation algorithm before the game starts, but is unable to determine the outcomes of the number generation algorithm until after the game.

The procedure for turning this concatenated string into a number mentioned in step 4 must also be publicly known. Provably Fair betting sites usually publish a page that explains exactly how they concatenate the inputs and how they turn those inputs into a number. The page includes enough detail to allow anyone to reproduce the algorithm and independently verify that the results were not manipulated. These pages usually also include a calculator that allows the user to verify game results using the hash of the server seed, the plaintext of the server seed, and the client seed.

# Caveats

The algorithm described above only works for singleplayer games.