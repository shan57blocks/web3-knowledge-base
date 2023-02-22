*Author: lily.hu*

## What is Ethers?

The ethers.js library aims to be a complete and compact library for interacting with the Ethereum Blockchain and its ecosystem. It enables us to easily interact with the Ethereum blockchain using Javascript.

## Installing and Importing

### Installing

npm: `npm install --save ethers` or `npm install -g ethers`

yarn: `yarn add ethers` or `yarn global add ethers`

### Importing

node.js: `const { ethers } = require("ethers");`

ES6 or TypeScript: `import { ethers } from "ethers";`

## Main Module Introduction

### Providers

A Provider is an abstraction of a connection to the Ethereum network, providing a concise, consistent interface to standard Ethereum node functionality.

The ethers.js library provides several provider sub-classes:

- JsonRpcProvider

The JSON-RPC API is a popular method for interacting with Ethereum and is available in all major Ethereum node implementations as well as many third-party web services
  - JsonRpcSigner
  - JsonRpcUncheckedSigner
  - StaticJsonRpcProvider

- API Providers

There are many services which offer a web API for accessing the Ethereum Blockchain. These Providers allow connecting to them, which simplifies development, since you do not need to run your own instance or cluster of Ethereum nodes. So ethers.js library provider the related providers:
  - EtherscanProvider
  - InfuraProvider
  - AlchemyProvider
  - CloudflareProvider
  - PocketProvider
  - AnkrProvider

- Other Providers
  - FallbackProvider
  - IpcProvider
  - JsonRpcBatchProvider
  - UrlJsonRpcProvider
  - Web3Provider
  - WebSocketProvider

[More](https://docs.ethers.org/v5/api/providers/)

## Signers

A Signer in ethers is an abstraction of an Ethereum Account, which can be used to sign messages and transactions and send signed transactions to the Ethereum Network to execute state changing operations.

The most common Signers you will encounter are:
- Wallet: It is a class which knows its private key and can can sign transactions and messages

- JsonRpcSigner: It is connected to a JsonRpcProvider (or sub-class) and is acquired using getSigner

[More](https://docs.ethers.org/v5/api/signer/)

## Contract Interaction

- Contract: A Contract object is an abstraction of a contract (EVM bytecode) deployed on the Ethereum network. It allows for a simple way to serialize calls and transactions to an on-chain contract and deserialize their results and emitted logs.

- ContractFactory: A ContractFactory is an abstraction of a contract's bytecode and facilitates deploying a contract.

[More](https://docs.ethers.org/v5/api/contract/)

## Utilities

### Application Binary Interface

An Application Binary Interface (ABI) is a collection of Fragments which specify how to interact with various components of a Contract.

[More](https://docs.ethers.org/v5/api/utils/abi/)

### Addresses

Explain addresses,formats and checksumming

[More](https://docs.ethers.org/v5/api/utils/address/)

### BigNumber

A BigNumber is an object which safely allows mathematical operations on numbers of any magnitude.

Most operations which need to return a value will return a BigNumber and parameters which accept values will generally accept them.

[More](https://docs.ethers.org/v5/api/utils/bignumber/)

### Constants

In addition to the commonly used utilities listed above, the ethers.js also providers many other utilities, you can find them by the official document.

[More](https://docs.ethers.org/v5/api/utils/constants/)

### Experimental

- BrainWallet: This class is offered to ensure older systems which used brain wallets can still recover their funds and assets

- EIP1193Bridge: The EIP1193Bridge allows a normal Ethers Signer and Provider to be exposed in as a standard EIP-1193 Provider, which may be useful when interacting with other libraries.

- NonceManager: The NonceManager is designed to manage the nonce for a Signer, automatically increasing it as it sends transactions

[More](https://docs.ethers.org/v5/api/experimental/)

## Practice Examples

There are some practices that guide you use ethers step by step. You can follow them to study how to use ethers in project.

[WTF 学院](https://wtf.academy/ether-start/)