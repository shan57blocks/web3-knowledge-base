# Wallet Technologies

*Author: shu@57blocks.com*

This document describes the implementation technologies of web3 wallet, which will help developers understand the working mechanism of web3 wallet more deeply.

## Overview

A common misconception about bitcoin is that bitcoin wallets contain bitcoin. In fact, the wallet contains only keys. The "coins" are recorded in the blockchain on the Bitcoin network. Users control the coins on the network by signing transactions with the keys in their wallets. In a sense, a bitcoin wallet is a keychain.

There are two primary types of wallets, distinguished by whether the keys they contain are related to each other or not.

* The first type is a nondeterministic wallet, where each key is independently generated from a random number. The keys are not related to each other. This type of wallet is also known as a JBOK wallet from the phrase "Just a Bunch Of Keys."

* The second type of wallet is a deterministic wallet, where all the keys are derived from a single master key, known as the seed. All the keys in this type of wallet are related to each other and can be generated again if one has the original seed. There are a number of different key derivation methods used in deterministic wallets. The most commonly used derivation method uses a tree-like structure and is known as a hierarchical deterministic or HD wallet.

    Deterministic wallets are initialized from a random sequence (entropy). To make these easier to use, random sequences are encoded as English words, also known as mnemonic code words.

### Deterministic (Seeded) Wallets

Deterministic, or "seeded," wallets are wallets that contain private keys that are all derived from a common seed, through the use of a one-way hash function. The seed is a randomly generated number that is combined with other data, such as an index number or "chain code" to derive the private keys. In a deterministic wallet, the seed is sufficient to recover all the derived keys, and therefore a single backup at creation time is sufficient. The seed is also sufficient for a wallet export or import, allowing for easy migration of all the user’s keys between different wallet implementations.

Type-1 deterministic (seeded) wallet: a deterministic sequence of keys derived from a seed shows a logical diagram of a deterministic wallet.
![](../../assets/images/Web3WalletsAndWalletAddress/deterministic-wallet.png)

### HD Wallets ([BIP-32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki)/[BIP-44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki))

Deterministic wallets were developed to make it easy to derive many keys from a single "seed". The most advanced form of deterministic wallets is the HD wallet defined by the [BIP-32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) standard. HD wallets contain keys derived in a tree structure, such that a parent key can derive a sequence of children keys, each of which can derive a sequence of grandchildren keys, and so on, to an infinite depth.

This tree structure is illustrated in Type-2 HD wallet: a tree of keys generated from a single seed.
![](../../assets/images/Web3WalletsAndWalletAddress/HD-wallet.png)

HD wallets offer two major advantages over random (nondeterministic) keys. First, the tree structure can be used to express additional organizational meaning, such as when a specific branch of subkeys is used to receive incoming payments and a different branch is used to receive change from outgoing payments. Branches of keys can also be used in corporate settings, allocating different branches to departments, subsidiaries, specific functions, or accounting categories.

The second advantage of HD wallets is that users can create a sequence of public keys without having access to the corresponding private keys. This allows HD wallets to be used on an insecure server or in a receive-only capacity, issuing a different public key for each transaction. The public keys do not need to be preloaded or derived in advance, yet the server doesn’t have the private keys that can spend the funds.

### Seeds and Mnemonic Codes ([BIP-39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki))

HD wallets are a very powerful mechanism for managing many keys and addresses. They are even more useful if they are combined with a standardized way of creating seeds from a sequence of English words that are easy to transcribe, export, and import across wallets. This is known as a mnemonic and the standard is defined by [BIP-39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki). Today, most bitcoin wallets (as well as wallets for other cryptocurrencies) use this standard and can import and export seeds for backup and recovery using interoperable mnemonics.

### Creating an HD Wallet from the Seed

Every key in the HD wallet is deterministically derived from this root seed, which makes it possible to re-create the entire HD wallet from that seed in any compatible HD wallet. This makes it easy to back up, restore, export, and import HD wallets containing thousands or even millions of keys by simply transferring only the mnemonic that the root seed is derived from.

Creating master keys and chain code from a root seed
![](../../assets/images/Web3WalletsAndWalletAddress/Creating-master-keys-and-chain-code-from-a-root-seed.png)

The root seed is input into the HMAC-SHA512 algorithm and the resulting hash is used to create a master private key (m) and a master chain code (c).

The master private key (m) then generates a corresponding master public key (M) using the normal elliptic curve multiplication process m * G that we saw in [pubkey].

#### Private child key derivation

HD wallets use a child key derivation (CKD) function to derive child keys from parent keys.

#### Using derived child keys

Child private keys are indistinguishable from nondeterministic (random) keys. Because the derivation function is a one-way function, the child key cannot be used to find the parent key. The child key also cannot be used to find any siblings. If you have the nth child, you cannot find its siblings, such as the n–1 child or the n+1 child, or any other children that are part of the sequence. Only the parent key and chain code can derive all the children. Without the child chain code, the child key cannot be used to derive any grandchildren either. You need both the child private key and the child chain code to start a new branch and derive grandchildren.

So what can the child private key be used for on its own? It can be used to make a public key and a Bitcoin address. Then, it can be used to sign transactions to spend anything paid to that address.

#### Public child key derivation

As mentioned previously, a very useful characteristic of HD wallets is the ability to derive public child keys from public parent keys, without having the private keys. This gives us two ways to derive a child public key: either from the child private key, or directly from the parent public key.

### References

[Wallet Technology Details](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch05.asciidoc#wallet-technology-details)

[How Cryptography Is Used in Cryptocurrency](https://www.worldcryptoindex.com/how-cryptography-is-used-cryptocurrency/)

[Mastering Bitcoin, 2nd Edition by Andreas M. Antonopoulos, Chapter 4. Keys, Addresses](https://www.oreilly.com/library/view/mastering-bitcoin-2nd/9781491954379/ch04.html)

[Mnemonic code words, based on BIP-39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)

[HD wallets, based on BIP-32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki)

[Multipurpose HD wallet structure, based on BIP-43](https://github.com/bitcoin/bips/blob/master/bip-0043.mediawiki)

[Multicurrency and multiaccount wallets, based on BIP-44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki)

## Typical wallet addresses

### BTC wallet address:

* Bitcoin wallet addresses have between 26 and 35 characters and consist of both letters and numbers. They start with either "1," "3," or "bc1." Here's an example of a Bitcoin address:
**1Lbcfr7sAHTD9CgdQo3HTMTkV8LK4ZnX71**

* With some cryptocurrencies, including Bitcoin, each address you generate is different. Previous addresses are still tied to your account and can be reused. 

### ETH wallet address:
* Ethereum addresses are 42-character hexadecimal addresses. They're generated using the last 20 bytes of the wallet's public key and by adding "0x" to the front. Here's an example of an Ethereum address:
**0x1ABC7154748D1CE5144478CDEB574AE244B939B5**

* With other cryptocurrencies, including Ethereum, wallet addresses don't change.

### Solana wallet address

* In Solana, the wallet address is the public key of a keypair. There are a variety of techniques for generating keypairs. The method you choose will depend on how you choose to store keypairs. Keypairs are stored in wallets. Before receiving tokens, you will need to create a wallet. Once completed, you should have a public key for each keypair you generated. The public key is a long string of base58 characters. Its length varies from 32 to 44 characters. Here's an example of an Solana address:
**E645TckHQnDcavVv92Etc6xSWQaq8zzPtPRGBheviRAk**