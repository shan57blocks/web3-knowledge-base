## Overview

### WHAT'S A TRANSACTION?
An Ethereum transaction refers to an action initiated by an externally-owned account(EOA), in other words an account managed by a human, not a contract. 

### HOW TO SEND A TRANSACTION?
- get a wallet
- have native native token as gas fee
- set a provider
- construct transaction
- sign  transaction
### HOW TO TRACK YOUR TRANSACTION?
If you are executing a tranction on Ethereum mainnet, the best way to track the status of the transaction is on [etherscan.io](https://etherscan.io/). Just input the transaction hash to check.

## Basics

### Accounts

There are two types of accounts, smart contract accounts and externally owned accounts (EOA):

`Externally owned accounts (EOA)` refer to accounts that humans manage, such as a personal Metamask or Coinbase wallet. This account is identified by a public key (also known as an account address) and is controlled by a private key. The public key is derived from the private key using a cryptographic algorithm. It's important to note that these accounts cannot store information other than your accounts balance and nonce.

`Smart contract accounts` (also known as contract accounts) also contain an address to balance mapping but differ because they can also include EVM code and storage. Contract accounts control themselves by the logic in the EVM code stored within the account.

Ethereum utilizies the elliptic curve digital signature algorithm (ECDSA) to prove authentication (i.e., prove that we have a private key for our public address) and verify that our transaction comes from the account signing the transaction and is not fraudulent.

### TRANSACTION OBJECT

A submitted transaction includes the following information:

`recipient` – the receiving address (if an externally-owned account, the transaction will transfer value. If a contract account, the transaction will execute the contract code)

`signature` – the identifier of the sender. This is generated when the sender's private key signs the transaction and confirms the sender has authorized this transaction

`nonce` - a sequentially incrementing counter which indicates the transaction number from the account

`value` – amount of ETH to transfer from sender to recipient (in WEI, a denomination of ETH)

`data` – optional field to include arbitrary data

`gasLimit` – the maximum amount of gas units that can be consumed by the transaction. Units of gas represent computational steps

`maxPriorityFeePerGas` - the maximum price of the consumed gas to be included as a tip to the validator

`maxFeePerGas` - the maximum fee per unit of gas willing to be paid for the transaction (inclusive of baseFeePerGas and maxPriorityFeePerGas)

Gas is a reference to the computation required to process the transaction by a validator. Users have to pay a fee for this computation. The gasLimit, and maxPriorityFeePerGas determine the maximum transaction fee paid to the validator. More on Gas.

The transaction object will look a little like this:

```
{
  from: "0xEA674fdDe714fd979de3EdF0F56AA9716B898ec8",
  to: "0xac03bb73b6a9e108530aff4df5077c2b3d481e5a",
  gasLimit: "21000",
  maxFeePerGas: "300",
  maxPriorityFeePerGas: "10",
  nonce: "0",
  value: "10000000000"
}
```
But a transaction object needs to be signed using the sender's private key. This proves that the transaction could only have come from the sender and was not sent fraudulently.

An Ethereum client like Geth will handle this signing process.

Example JSON-RPC call:

```
{
  "id": 2,
  "jsonrpc": "2.0",
  "method": "account_signTransaction",
  "params": [
    {
      "from": "0x1923f626bb8dc025849e00f99c25fe2b2f7fb0db",
      "to": "0x07a565b7ed7d7a678680a4c162885bedbb695fe0",
      "value": "0x1234"
      "input": "0xabcd",
      "nonce": "0x0",
      "gas": "0x55555",
      "maxFeePerGas": "0x1234",
      "maxPriorityFeePerGas": "0x1234",
    }
  ]
}

```

### The data field
The vast majority of transactions access a contract from an externally-owned account. Most contracts are written in Solidity and interpret their data field in accordance with the application binary interface (ABI).

The first four bytes specify which function to call, using the hash of the function's name and arguments. You can sometimes identify the function from the selector using this database.

The rest of the calldata is the arguments, encoded as specified in the ABI specs.

For example, lets look at [this transaction](https://etherscan.io/tx/0xd0dcbe007569fcfa1902dae0ab8b4e078efe42e231786312289b1eee5590f6a1). Use Click to see More to see the calldata.

The function selector is `0xa9059cbb`. There are several known functions with this signature. In this case the contract source code has been uploaded to Etherscan, so we know the function is `transfer(address,uint256)`.

The rest of the data is:
```
0000000000000000000000004f6742badb049791cd9a37ea913f2bac38d01279
000000000000000000000000000000000000000000000000000000003b0559f4
```
According to the ABI specifications, integer values (such as addresses, which are 20-byte integers) appear in the ABI as 32-byte words, padded with zeros in the front. So we know that the to address is `4f6742badb049791cd9a37ea913f2bac38d01279`. The value is 0x3b0559f4 = 990206452.

### TRANSACTION RESPONSE OBJECT

Example response:

```
{
  "jsonrpc": "2.0",
  "id": 2,
  "result": {
    "raw": "0xf88380018203339407a565b7ed7d7a678680a4c162885bedbb695fe080a44401a6e4000000000000000000000000000000000000000000000000000000000000001226a0223a7c9bcf5531c99be5ea7082183816eb20cfe0bbc322e97cc5c7f71ab8b20ea02aadee6b34b45bb15bc42d9c09de4a6754e7000908da72d48cc7704971491663",
    "tx": {
      "nonce": "0x0",
      "maxFeePerGas": "0x1234",
      "maxPriorityFeePerGas": "0x1234",
      "gas": "0x55555",
      "to": "0x07a565b7ed7d7a678680a4c162885bedbb695fe0",
      "value": "0x1234",
      "input": "0xabcd",
      "v": "0x26",
      "r": "0x223a7c9bcf5531c99be5ea7082183816eb20cfe0bbc322e97cc5c7f71ab8b20e",
      "s": "0x2aadee6b34b45bb15bc42d9c09de4a6754e7000908da72d48cc7704971491663",
      "hash": "0xeba2df809e7a612a0a0d444ccfa5c839624bdc00dd29e3340d46df3870f8a30e"
    }
  }
}
```
the `raw` is the signed transaction in Recursive Length Prefix (RLP) encoded form
the `tx` is the signed transaction in JSON form
With the signature hash, the transaction can be cryptographically proven that it came from the sender and submitted to the network.


### TYPES OF TRANSACTIONS

On Ethereum there are a few different types of transactions:

`Regular transactions`: a transaction from one account to another.

`Contract deployment transactions`: a transaction without a 'to' address, where the data field is used for the contract code..

`Execution of a contract`: a transaction that interacts with a deployed smart contract. In this case, 'to' address is the smart contract address.

Generally, every Ethereum transaction falls into one of three groups, as shown below:

`Normal Transactions` – Whenever an EOA (externally owned account) sends ETH to another EOA, we call it a “normal transaction”. EOAs are accounts held by humans rather than contracts and are usually called wallets. To check your blockchain transactions and analyze your projects, you need to have an account in a block explorer. Etherscan, Etherchain, and the “Blockchain” explorer from Ethereum are some of the well-known block explorers out there. If you are using Etherscan, you can check your “Normal Transactions” section under the “Transaction” tab. 

`Internal Transactions` – In these types of transactions, smart contracts play the role of an intermediary and transfer ETH between accounts. In Etherscan, you can see the internal transactions under the “Internal Txns” tab. 

`Token Transfers` – This category belongs to the transactions of tokens compatible with ERC-20 and ERC-721 protocols. You can check these transactions under the “ERC20 Token Txns” or “ERC721 Token Txns” tabs in Etherscan.

#### On gas

As mentioned, transactions cost gas to execute. Simple transfer transactions require 21000 units of Gas.

So for Bob to send Alice 1 ETH at a baseFeePerGas of 190 gwei and maxPriorityFeePerGas of 10 gwei, Bob will need to pay the following fee:

(190 + 10) * 21000 = 4,200,000 gwei
--or--
0.0042 ETH

Bob's account will be debited -1.0042 ETH (1 ETH for Alice + 0.0042 ETH in gas fees)

Alice's account will be credited +1.0 ETH

The base fee will be burned -0.00399 ETH

Validator keeps the tip +0.000210 ETH

Gas is required for any smart contract interaction too.

Diagram showing how unused gas is refundedDiagram adapted from Ethereum EVM illustrated

Any gas not used in a transaction is refunded to the user account.

### TRANSACTION LIFECYCLE

Once the transaction has been submitted the following happens:

1.Once you send a transaction, cryptography generates a transaction hash: `0x97d99bc7729211111a21b12c933c949d4f31684f1d6954ff477d0477538ff017`

2.The transaction is then broadcast to the network and included in a pool with lots of other transactions.

3.A validator must pick your transaction and include it in a block in order to verify the transaction and consider it "successful".

4.As time passes the block containing your transaction will be upgraded to "justified" then "finalized". These upgrades make it much more certain that your transaction was successful and will never be altered. Once a block is "finalized" it could only ever be changed by an attack that would cost many billions of dollars.

### Transaction States

- Pending: Transactions broadcasted to the network waiting to be mined. If the transaction is taking longer than expected, it's possible that your gas fee is not high enough to meet execution at the current time.

- Queued: A transaction that cannot be mined yet due to another pending transaction in the queue first or an out of sequence nonce.

- Cancelled: Can no longer be mined. Replaced by a transaction with a higher gas fee, same nonce value, and a null value for the data and/or value field.

- Replaced: Can no longer be mined. Used to replace current pending orders for faster execution or modification of values and data. This also consists of using the same nonce as the transaction you want to cancel and a higher gas fee.

- Failed: A transaction that resulted in an error due to a revert error, bad instructions, illogical code, or not enough gas to run the remainder of a function call.

#### Difference between Pending and Queued Transactions

A transaction on Ethereum consists of different components such as a cryptographically signed signature (deriving from the sender's private key), a set of instructions, a node to be broadcasted on, and a fee that will go to a miner. Once a transaction is broadcasted to the network, it can go into two different states depending on the value used in the transactions nonce field. The states fall into these categories:

- `Pending` - Transactions available to be processed and included in the next block.
- `Queued` - Transactions out of sequence that cannot be included in the next block.

A transaction must include a nonce. The nonce value in a transaction is set by the sender and allows for the ordering of transactions while also preventing replay attacks. All transactions submitted from an account must follow its nonce sequence to put in a pending transaction state.

For example, say an account sends its first transaction and has its nonce set to 0. The second transaction sent from the account should contain a nonce value of 1. The third transaction sent is expected to have a nonce value of 2 and so on, incrementing by one each transaction. In a scenario where you have submitted multiple transactions, and the first transaction (i.e., nonce=0) is still pending, the remaining transactions from the sending account (with nonce one and greater) would be in a queued state until the first transaction has been processed.

Alternatively, if an account accidentally sends a transaction with an out-of-sequence nonce, the said transaction would stay queued until the transaction is replaced with the correct nonce or until another transaction with the missing nonce(s) is submitted and processed first.

There are two reasons why a transaction can be in a queued state:

There can be existing pending transaction(s) that must be processed first.
The transaction has been submitted with an out of sequence nonce.

#### What transaction lifecycle states can a mempool transaction be in?
Traditionally, mempool transactions fall into one of the following three buckets:

- `Pending Transactions`
Transactions that have been submitted to the mempool and are waiting to be included in the next block mined by a miner. Learn more about debugging pending transactions..

- `Mined Transactions`
Transactions that have been selected and are included in the latest block by a miner. The results of these transactions are then broadcasted to the entire network. Mined transactions can have two statuses:

`Success`

These transactions are successfully executed and modify state on-chain. The status field for a successful transaction is 0x1.

- `Failure/Execution Reverted`
These transactions are not successfully executed but are still included in the block. This can occur if the execution process hits an error, runs out of gas, or encounters some other issue. The status field for a failed transaction is 0x0.

To check whether a mined transaction was successful or failed you can call `eth_getTransactionReceipt` passing in your transaction hash. In the payload, you will find a status field which will be 0x0 for failed and 0x1 for success.

`Dropped Transactions`
Transactions that have failed to be confirmed. This could happen because the transaction failed certain validation tests, the nonce was incorrect, the submitted gas price was too low and it timed out, or a number of other errors. Dropped transactions return their assets and gas fees to the sender, as if the transaction never happened.

Need help troubleshooting dropped transactions? Watch our tutorial on how to fix pending or stuck transactions with Alchemy’s Mempool Watcher.

#### What are Dropped & Replaced transactions?
A new category has become a common feature request by developers. When a transaction is dropped, the sender will oftentimes send a replacement transaction with the same nonce value to “replace” that failed transaction.

If the second transaction is confirmed onto the blockchain (e.g. by sending a new transaction with the same nonce and a higher gas price), the “dropped” transaction will be moved into the new transaction status category known as “Dropped & Replaced”.

Similarly, if multiple transactions are simultaneously sent with the same nonce value, typically the transaction with a higher transaction fee will be selected for confirmation onto a block. The other transactions will fall into the “Dropped & Replaced” category.

This transaction status is useful for smart contract developers as it allows them to track which transactions have been successfully re-broadcasted to the blockchain network (“dropped and replaced”) and which dropped transactions still need to be re-broadcasted (“dropped”).

### Useful Websites
https://www.4byte.directory/
https://chainlist.org/

### Reference Documents
https://ethereum.org/en/developers/docs/transactions