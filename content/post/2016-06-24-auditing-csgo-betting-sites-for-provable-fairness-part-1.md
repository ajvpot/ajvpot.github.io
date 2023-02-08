---
author: Alex Vanderpot
categories:
- Uncategorized
date: "2016-06-24T04:48:37Z"
guid: https://vanderpot.com/?p=72
id: 72
title: Auditing A CS:GO Betting Site for Provable Fairness
url: /2016/06/auditing-csgo-betting-sites-for-provable-fairness-part-1/
---

Provable fairness is one of the building blocks of modern online gambling. Many Bitcoin casinos have popped up that use “provably fair” number generation algorithms. These algorithms guarantee that the numbers generated have not been influenced by either party in a way that is favorable for them. For a more detailed explanation of these systems, read [this blog post](https://vanderpot.com/2016/06/basics-of-provable-fairness/). Recently, I have been introduced to the Counter-Strike: Global Offensive gambling scene. These online casinos have sprouted up from a legal loophole. Apparently, gambling with virtual items (CS:GO skins) that hold value on a market is not illegal. However, these items can be quickly traded for cash.

Many of these CS:GO gambling sites claim to be provably fair. I will be auditing these claims. In this post, I will provide a description of the provable fairness algorithm this website uses and some possible attacks that either the server or client could use. If this website had vulnerabilities that the client could exploit, the impact would be astronomical. Clients could predict the results of their rolls before they happened and use that information to only make rolls that have a favorable outcome for the client. Attacks that can be used by the server could allow the website operator to scam users and cause them to lose more than normal.

# CSGOWild.com

CSGOWild has two games, I will be looking at both.

## Coin Flip

CSGOWild’s coin flip game mode allows you to flip a coin against another user. Their [provably fair page](http://csgowild.com/provably-fair) describes their algorithm as follows.

1. The server generates a “salt” (this is an incorrect use of the word salt) and a “winning percentage.”
2. The “salt” and “winning percentage” are concatenated with a : and hashed. This is the “round hash.”
3. The “round hash” is shared with both users taking place in the game.
4. After the game is over, the round hash and the winning percentage are shared with both users.

There are several problems with this process. The most blatant one being that the server does not take any input from the clients while creating the round hash or generating the winning percentage. The server knows which player bet on each side of the coin before it decides the winning percentage, so **the server can choose which player will win before the coin is flipped**. If this manipulation was combined with fake players that were playing for the house, CSGOWild could make those players win all of the bets that they made.

## Roulette

CSGOWild’s roulette game does not have an entry on their Provable Fairness description page. I looked at the messages being sent over the WebSocket that the client uses to communicate with the server and found that there are no precautions being taken against the server influencing results. **The server can choose any result at any time. This game mode is not provably fair at all.**