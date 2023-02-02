# Bitcoin Transaction

## What is Bitcoin Transaction？

A transaction exists as a record of the transfer of bitcoin. All transactions are recorded in blocks on the blockchain. Most users use wallets to send and receive Bitcoin transactions. Wallets do all of the technical work in the background so that users can simply specify an address and an amount to send to that address.

When a transaction is ready, it is broadcast to nodes on the Bitcoin network. These nodes keep the transaction in a pool of pending transactions called the mempool until miners add it to a block. Only once a transaction is added to a block is it confirmed. It is a safe practice to wait until a transaction has been in the blockchain for at least 6 blocks to consider it settled with finality.

Let’s walk through an example transaction: Alice owns a UTXO worth 1 BTC and wishes to pay Bob 0.4 BTC. Thus, she uses the 1 BTC UTXO as an input. In order to send Bob exactly 0.4 BTC, Alice creates two outputs: the first to Bob, in the amount of 0.4 BTC, and the second back to herself, in the amount 0.59 BTC. This means that she paid a 0.01 BTC transaction fee.

> Key Fact: the fee of a Bitcoin transaction is not an output of the transaction.

The fee is not itself an output. It is implied by the sum of the inputs (1 BTC) minus the sum of the outputs (0.4 + 0.59 = 0.99 BTC) and is collected by the miner.
Lastly, Alice uses the private key controlling the 1 BTC UTXO to sign the transaction before broadcasting it to the network. When this transaction is added to the blockchain, the 1 BTC UTXO will be destroyed, and two new UTXOs in the amounts of 0.4 BTC and 0.59 BTC will be created, belonging to Bob and Alice respectively.

KEY HIGHLIGHTS

* A Bitcoin transaction is a transfer of bitcoin from one address to another. The valid transaction must be signed by the sender.
* Bitcoin does not have accounts. Instead, pieces of Bitcoin of arbitrary size are all associated with an address, which is controlled by the owner of that bitcoin. These pieces of Bitcoin are called Unspent Transaction Outputs (UTXOs).
* All Bitcoin transactions are published to the mempool, where they are considered 'pending'. When a miner adds a transaction to a block, it is then considered confirmed.

## What Is a Bitcoin Transaction?

A transaction is a transfer of Bitcoin value on the blockchain. In very simple terms, a transaction is when participant A gives a designated amount of Bitcoin they own to participant B.

Transactions are created through mobile, desktop or hardware wallets.

### How Does A Bitcoin Transaction Work?

For Bitcoin users, sending a transaction is as simple as entering an amount and an address in their wallet and pressing send. They don’t have to worry about the technicalities of how it works. Many users are curious how it works in practice though.

Bitcoin makes use of public-key cryptography to ensure the integrity of transactions created on the network. In order to transfer bitcoin, each participant has pairs of public keys and private keys that control pieces of bitcoin they own. A public key is a series of letters and numbers that a user must share in order to receive funds. In contrast, a private key must be kept secret as it authorizes the spending of any funds received by the associated public key.

Key Fact: Both addresses and public keys can be used to receive bitcoin, but addresses are prefered for security and brevity.
The terms address and public key are often used interchangeably. An address is a representation of a public key, used for security and brevity.
Using the private key associated with their bitcoin, a user can sign transactions and thereby transfer the value to a new owner. The transaction is then broadcast to the network to be included in the blockchain.

Warning: anyone who possesses your private keys has access to your bitcoin.
Anyone who possesses your private keys has access to your bitcoin.

## Overview of a Bitcoin Transaction

To better illustrate how value is transferred in the Bitcoin network, we will walk through an example transaction, where Alice sends .05 bitcoin to Bob.

Under the hood, a transaction consists of three main parts: inputs, outputs, and a signature.
Inputs are simply pieces of bitcoin called UTXOs which the payer chooses to spend.
Outputs send a specified amount of bitcoin to a specified address, creating a new UTXO.
A transaction can contain any number of inputs and outputs. Lastly, in order for the transaction to be valid, the payer must sign the transaction, thereby proving ownership of the inputs they are attempting to spend. This signature is produced using the payer’s private keys.

At a high level, a transaction has three main parts:

* Inputs. The bitcoin address that contains the bitcoin Alice wants to send. To be more accurate, it is the address from which Alice had previously received bitcoin to and is now wanting to spend.
* Outputs. Bob’s public key or bitcoin address.
* Amounts. The amount of bitcoin Alice wants to send.

Key Fact: A transaction can contain multiple inputs and outputs.

A transaction can contain multiple inputs and outputs. As long as each output has an associated amount and the input amounts total more than the output amounts, the transaction is valid.

In order for Alice to send the .05 bitcoin to Bob, she signs a message with the transaction details using her private key. The message contains the input, output, and amount as described above. The transaction is then broadcast to the rest of the Bitcoin network where nodes verify that Alice’s private key is able to access the inputs (by checking that Alice’s private key matches the public key she is claiming to own).

Once a transaction is broadcasted to a node, this node then passes it along the network until it reaches a mining node. Miners will then order this transaction into what is called a block template. This is a blueprint for the block which the miner is attempting to add to the blockchain. If a miner finds the next block in the chain, then this block template is mined and becomes an immutable block on the blockchain. Finally, this block is broadcasted to the network’s nodes who will include it in their copy of the chain.

## Glossory

### Change Output

Bitcoin does not use accounts and balances. Instead, pieces of bitcoin, called UTXOs, are owned by individuals. These can be likened to physical bills in that when they are spent, they will usually require change to be given as their amount will almost never match the amount being paid.

When a user creates a transaction, they select an input, a UTXO which they own, and create outputs. One output will go to the receiver’s address and the other output will be returned to the sender’s wallet, usually via a different address. The amount for this second output will be the change, which will amount to the sum of the inputs minus the amount spent in the first output and the transaction fee.

### UTXO Set

The UTXO set is the comprehensive set of all UTXOs existing at a given point in time. The sum of the amounts of each UTXO in this set is the total supply of existing bitcoin at that point of time.

Bitcoin is special as a money in that anyone can verify the total supply at any time in a trustless manner. All nodes maintain identical copies of the UTXO set. When a new block is created, the UTXO set is updated as some UTXOs were spent and new ones were created.

The UTXO set is also important because it allows all nodes in the Bitcoin network to detect and reject attempted double spends, wherein someone attempts to spend the same bitcoin twice. Nodes must store the entire UTXO at all times in order to determine which bitcoin exist, and thus can be spent, at any given point in time.

### Coin Selection

Coin selection is the process of choosing a subset of the UTXOs owned by a wallet in order to create and fund a transaction. When creating a transaction on behalf of a user, a wallet must select specific UTXOs as inputs in the transaction.

For example, if Alice wishes to pay Bob 1 BTC and her wallet contains 5 BTC in various amounts, her wallet must determine which UTXOs to spend. This decision is not trivial, and depends on the priority of the user. Some coin selection methods prioritize spending smaller outputs to avoid dust accumulation while others spend large outputs to pay lower fees. Still others prioritize privacy or avoiding change outputs.

Coin selection is usually dictated by an algorithm built into a wallet, but some wallets allow users to dictate their own coin selection preferences to suit their needs.

### Bitcoin Transaction Fees

All Bitcoin transactions must pay a fee to be included in the blockchain. This forms a part of the incentive for miners to mine. The higher the fee a transaction pays, the more incentive miners will have to mine the transaction, meaning it will be confirmed faster. Because miners can only fit 4MB of data in each block, they rate transactions based on the fee-to-byte ratio, not the total fee paid. Thus, most wallets will display fees in terms of sats/vByte.

Bitcoin transaction fees fluctuate wildly, and many transactions pay high fees in order to guarantee rapid confirmation, while others pay low fees and simply wait longer for confirmation. In the future, most bitcoiners expect fees to rise as demand to transact on the network grows. There are a few methods for saving on fees, including UTXO consolidation, batching transactions, and using the latest transaction types, especially SegWit.

### Dust

If a piece of bitcoin, called a UTXO, is small enough, it may cost more in fees to spend it than it is worth. As fees rise, more and larger amounts of bitcoin may become dust. To avoid bitcoin turning into dust, it is a good practice to consolidate very small amounts of bitcoin into a single larger amount at a time when bitcoin fees are low.

### Batching

Batching involves consolidating multiple payments into a single transaction with many outputs. Because Bitcoin fees are paid based on how much data the transaction uses, combining multiple transactions into a single transaction can lower data overhead and thus save on fees.

For example, if Alice wants to pay Bob 0.5 BTC, Charlie 0.3 BTC, and David 0.2 BTC, she can create a transaction with a 1 BTC input and 3 outputs instead of creating 3 transactions with 2 outputs each—one for the payee and one for change output.

The advantages of batching increases with scale. For example, an exchange wishing to serve 100 client withdrawal requests can either submit 100 transactions, or a single transaction with 100 different outputs. The latter option will offer significant fee savings.

### Coinbase Transaction

A coinbase transaction is the first transaction in each block. The coinbase transaction distributes the block subsidy, which is currently 6.25 BTC per block, and also collects the cumulative fees of all transactions in the block.

Since this transaction is creating new bitcoin, the coinbase transaction is valid without any inputs. To see an example, check out this coinbase transaction in Block #650,000 on [Blockstream](https://blockstream.info/tx/8143b3b341f665b22adcb8489158356c03f7c93cf4e4fa673d8518fa0fed95e4): there will be no inputs, and the single output will be of the amount 6.25 BTC plus the 0.244131 BTC of fees the miner collected.

### Block Reward

The block reward is a combination of the block subsidy and all transaction fees paid by transactions in a specific block. When miners mine a block, they receive a block subsidy in the form of newly minted bitcoin. All transactions also include a fee, which miners collect. The block reward is the sum of these two amounts. As block subsidies are cut in half every four years, fees will slowly become a greater portion of the block reward. The term block reward and block subsidy are occasionally used interchangeably.

The block reward is paid out in the coinbase transaction of each block. This special transaction is the first transaction in every block, and it has no inputs. The output of a coinbase transaction cannot be spent for 100 blocks, so miners can only spend their block reward after a 100 block cooldown.

## Further Readings

[crypto.com](https://crypto.com/university/how-do-bitcoin-transactions-work)
[bitcoin.com](https://www.bitcoin.com/get-started/how-bitcoin-transactions-work/)
[bitcoin.org](https://developer.bitcoin.org/devguide/transactions.html)
[xangle.io](https://xangle.io/en/insight/research/62a830eee74de2fd402eafe3)
[aprendeblockchain](https://aprendeblockchain.wordpress.com/a-comparison-between-utxo-and-account-based-models/)
[horizen](https://www.horizen.io/blockchain-academy/technology/expert/utxo-vs-account-model/)

## Transaction Data

Every block must include one or more transactions. The first one of these transactions must be a coinbase transaction, also called a generation transaction, which should collect and spend the block reward (comprised of a block subsidy and any transaction fees paid by transactions included in this block).

The UTXO of a coinbase transaction has the special condition that it cannot be spent (used as an input) for at least 100 blocks. This temporarily prevents a miner from spending the transaction fees and block reward from a block that may later be determined to be stale (and therefore the coinbase transaction destroyed) after a block chain fork.

Blocks are not required to include any non-coinbase transactions, but miners almost always do include additional transactions in order to collect their transaction fees.

All transactions, including the coinbase transaction, are encoded into blocks in binary raw transaction format.

The raw transaction format is hashed to create the transaction identifier (txid). From these txids, the merkle tree is constructed by pairing each txid with one other txid and then hashing them together. If there are an odd number of txids, the txid without a partner is hashed with a copy of itself.

The resulting hashes themselves are each paired with one other hash and hashed together. Any hash without a partner is hashed with itself. The process repeats until only one hash remains, the merkle root.

For example, if transactions were merely joined (not hashed), a five-transaction merkle tree would look like the following text diagram:

       ABCDEEEE .......Merkle root
      /        \
   ABCD        EEEE
  /    \      /
 AB    CD    EE .......E is paired with itself
/  \  /  \  /
A  B  C  D  E .........Transactions
As discussed in the Simplified Payment Verification (SPV) subsection, the merkle tree allows clients to verify for themselves that a transaction was included in a block by obtaining the merkle root from a block header and a list of the intermediate hashes from a full peer. The full peer does not need to be trusted: it is expensive to fake block headers and the intermediate hashes cannot be faked or the verification will fail.

For example, to verify transaction D was added to the block, an SPV client only needs a copy of the C, AB, and EEEE hashes in addition to the merkle root; the client doesn’t need to know anything about any of the other transactions. If the five transactions in this block were all at the maximum size, downloading the entire block would require over 500,000 bytes—but downloading three hashes plus the block header requires only 140 bytes.

Note: If identical txids are found within the same block, there is a possibility that the merkle tree may collide with a block with some or all duplicates removed due to how unbalanced merkle trees are implemented (duplicating the lone hash). Since it is impractical to have separate transactions with identical txids, this does not impose a burden on honest software, but must be checked if the invalid status of a block is to be cached; otherwise, a valid block with the duplicates eliminated could have the same merkle root and block hash, but be rejected by the cached invalid outcome, resulting in security bugs such as CVE-2012-2459.
