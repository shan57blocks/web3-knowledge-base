# UTXO VS. ACCOUNT MODEL

For digital money to be useful, it needs to be transferable. The transfer of money on a blockchain is initiated by the owner, creating a transaction. This transaction informs the network about how much money is changing hands and who the new owner is.

We’ve explained what data comprises a transaction when we looked at the blockchain as a data structure. When we talked about public key cryptography, we covered how ownership is proven and verified on a blockchain, a key aspect of enabling secure transactions.

Here, we’ll look at the accounting/balance models used in blockchains. Most blockchains use the UTXO model for accounting. The second method to track user balances, as applied in Ethereum, is the account model.

We will start by looking at their similarities and then dive deep into each model individually. Lastly, we will compare the two models and briefly show how they can be combined to create a hybrid system.

## The Blockchain is a State Machine

Before we get into the different balance models, it makes sense to take a step back and look at the blockchain in more general terms - as a state machine.

A system is described as stateful, only if it is configured to remember preceding events or user interactions. The retained information is defined as the state of the system. Hence, a blockchain qualifies as a stateful system. Its entire purpose is to record past events and user interactions. With each new block the system undergoes a state transition that happens according to the state transition logic defined in its protocol.

Every blockchain, no matter if it uses the UTXO or account model, follows this scheme: The user interactions, mostly transactions, are broadcast to the network, and with each new block, a set of them is permanently recorded. The balances of the transacting parties are updated when the system transitions to the new state.

The difference between the UTXO and the account model lies in the way the bookkeeping is handled. With bookkeeping, we mean recording the state and transitioning from one state to another.

### Recording the State

The first significant difference between the two balance models is how the state of the system is recorded.
In the UTXO model, the movement of assets is recorded as a directed acyclic graph (DAG) between addresses,
In the account model maintains a database of network states.

![RECORD_THE_STATE_OF_THE_SYSTEM](.gitbook/../../../.gitbook/assets/RECORD_THE_STATE_OF_THE_SYSTEM.jpg)

In the UTXO model, the entire graph of transaction outputs, spent and unspent, represents the global state.
In the account model, only the current set of accounts and their balances represents the global state.

The account model updates user balances globally.
The UTXO model only records transaction receipts. In the UTXO model, account balances are calculated on the client-side by adding up the available unspent transaction outputs (UTXOs).

### The UTXO Model

The UTXO model does not incorporate accounts or wallets at the protocol level. The model is based entirely on individual transactions, grouped in blocks. We can compare this to people holding certain amounts of cash.

Since there is no concept of accounts or wallets on the protocol level, the “burden” of maintaining a user’s balance is shifted to the client-side. Wallets maintain a record of all addresses controlled by a user and monitor the blockchain for all associated transactions. The sum of all unspent transaction outputs it can control determines the current balance.

#### State Transitions in the UTXO Model

Each transaction in the UTXO model can transition the system to a new state, but transitioning to a new state with each transaction is infeasible. All network participants must stay in sync on the current state. Designing a consensus mechanism that keeps all nodes synchronized becomes harder, when state transitions happen more frequently. This becomes intuitive when you consider that the time interval between blocks gives nodes the chance to download the most recent block and process it.

The shorter the period for nodes to update the state, the higher the chance of reaching an inconsistent state where some nodes have a different view of past events than others. As a result, transactions are batched into blocks, and each new block presents a system state transition.

## The Account Model

The account-based transaction model represents assets as balances within accounts, similar to bank accounts. Ethereum uses this transaction model. There are two different types of accounts:

Private key controlled user accounts and
Contract code-controlled accounts.
When you create an Ether wallet and receive your first transaction, a private key controlled account is added to the global state and stored across all nodes on the network. Deploying a smart contract leads to the creation of a code controlled account. Smart contracts can hold funds themselves, which they can redistribute according to the conditions defined in the contract logic. Every account in Ethereum has a balance, storage, and code-space for calling other accounts or addresses.

To prevent replay attacks, each transaction in the account model has a nonce attached. A replay attack is when a payee broadcasts a fraudulent transaction in which they get paid a second time. If the fraudulent transaction were to be successful, the transaction would be executed a second time - it is replayed - and the sender would be charged twice the amount they wanted to transfer.

To combat this behavior, each account in Ethereum has a public viewable nonce that is incremented by one with each outgoing transaction. This prevents the same transaction being submitted to the network more than once.

### Transaction fees

Transaction fees also work differently.
In the UTXO model, the transaction fee’s size is estimated by the wallet based on the amount of data recorded on-chain. Miners can only place a limited amount of data within a block, and by using the metric ‘money per amount of data,’ miners can determine which transactions to include in the block. They will typically pick the transactions with the highest fees per byte.
In the account model: They are calculated based on the number of computations required to complete the state transition. Ethereum set out to be a world computer. Hence they decided that fees should be based on the number of computational resources consumed rather than storage capacity taken.

The global state in the UTXO model is the set of all transaction outputs. The global state is always the entire graph of UTXOs. The state in the account model is the list of accounts and their balances. So in the second graphic, the global state (n+3) is this list of 3 accounts (A, B, and C) and their balances.

The main difference comes down to the global state in the UTXO model being only extended with new UTXOs, whereas in the account model, the global state is updated and balances change.

### State Transitions in the Account Model

The account model keeps track of all balances as a global state. This state can be understood as a database of all accounts, private keys, and contract-code controlled along with their current balances of the different assets on the network.
In a straightforward model, a transaction presents an event that triggers a state transition of the blockchain subject to the state transition logic. Just like in the UTXO model, it is infeasible to transition the system to a new state with every transaction without risking an inconsistent state. Transactions are also batched into blocks in the account model, and with each new block, the system transitions to a new state. Just like we did before, we consider a simple example where a single transaction transitions the system to a new state below.

Account model

The PubKey and Signature Script do not exist in account-based blockchains. The verification of signatures in account-based blockchain, Ethereum for example, is based on three parameters, r, s, and V provided by the sender. These three values comprise the signature. Solidity, the programming language used in Ethereum, provides a method, ecrecover that returns an address given these parameters. If the returned address matches the sender’s address, the signature, and in return, the transaction is valid.

Where in the UTXO model part of the verification process is checking if a transaction output in unspent, nodes in the account model check if the sender’s balance is larger than or equal to the transferred amount. This is true for the native asset of the chain, for example Ether, as well as all other tokens on the network.

A transaction in the account-based model is an instruction for how to transition two or more accounts to the next state. The actual transition is executed by the nodes. Because the final state is not specified in the transaction, the resulting transaction size is a lot smaller than in the UTXO model.

The state of accounts in Ethereum is not stored on the blockchain but computed and stored locally by the nodes. The blockchain only stores the instructions, read as transactions), for how the system should transition from one state to another.

## Comparing the UTXO and Account Model

Below, we will compare the strengths and weaknesses of the UTXO and account model. We will start by comparing them at a high-level computational view, and then move onto scalability, privacy, smart contract capabilities, and more.

In short, The UTXO model is a verification model. This means users submit transactions that specify the results of the state transition, defined as new transaction outputs spendable by the receiver(s). Nodes then verify if the consumed inputs are unspent and if the signature(s) satisfy the spending conditions.

The account model, on the other hand, is a computational model. In this model, users submit transactions instructing nodes on what state transitions should look like. The network then computes the new state based on the instructions. This method comes with specific implications regarding second layer scalability solutions like state channels and sharding.

- Scalability
There are several approaches we can use to compare the scalability of the UTXO and the account model. One way is to focus on the overall storage requirements of each system. Another way is to consider which model is better suited for the deployment of second-layer technologies on top of the main blockchain.

One second layer technology, state and payment channels, moves the exchange of data from the blockchain to a dedicated trustless network of bidirectional communication channels.

The other approach that could arguably be referred to as a second layer technology is sharding. Sharding is a term originating from the traditional database world. Sharding describes partitioning a database into several shards in order to keep each individual partition more performant, in turn improving the entire system. Horizen’s sidechain can be considered a sharding mechanism.

We’ll now compare both accounting methods and will assume that both systems have similar user and transaction counts.

- Size of the Blockchain
The account model has more efficient memory usage. Storing a single account balance saves memory compared to storing several UTXOs that comprise a user’s total balance. Transactions in the account model are also smaller in size because they only specify the sender, receiver, the transfer amount, and a single digital signature. Additionally, just by doing away with change outputs, a lot of data can be saved in the account model.

On a conceptual level, this is intuitive. Since a UTXO transaction specifies the state after the transition, the newly generated transaction outputs), it needs to include more data than an account transaction. It may also consume several UTXOs as inputs, whereas the account transaction only specifies which account balance to deduct an amount from. To give you an idea, Ethereum’s account model takes about 100 bytes, whereas a UTXO transaction in Horizen takes about 200-300 bytes.

This also means that it’s faster to get new nodes online in a system running the account model because less data is needed to get them in sync. The number of accounts will generally be much smaller than the total UTXO set in a comparably sized system.

- State and Payment Channel Constructions
Currently, the most advanced payment channel construction is the Lightning Network on Bitcoin. It uses a proof submission and verification mechanism as assets move into and out of the second layer. As mentioned above, the UTXO model is essentially a verification model, whereas the account model is a computational model. Hence, a UTXO construction is more suitable for these types of scalability approaches.

- Sharding
Partitioning a blockchain into shards or sidechains is also easier while using the UTXO model. Aggregating spendable transaction outputs and defining the outputs happens on the client-side, reducing the stress on the overall system. In the account model, every node has to localize the sender’s and receiver’s account across different shards and edit both.

Of course, there is more to sharding than these rather straightforward modifications, and using one balance model over the other comes with second and third-order effects. Generally, the UTXO model allows data structure partitioning more simply.

- Privacy
When it comes to privacy, there are merits to both the UTXO and the account model. The UTXO model makes it harder to link transactions, whereas the account model provides better fungibility.

When change addresses are consequently used in the UTXO model, it makes tracking the ownership of coins harder compared to the account model. A newly generated address doesn’t have a known owner and requires advanced chain analysis to be linked to a single user. The account model implicitly encourages address reuse and hence makes creating a transaction history for a single user easier.

With regard to fungibility, the account model offers better privacy. There is complete transparency of UTXO movements, read as assets, in the UTXO model when no privacy-preserving techniques are applied. However, the account model comes with a built-in “coin mixer” of sorts. When an account is funded with several transactions, the result is a single balance. When a payment from this account is made, an observer cannot determine which of the incoming coins is being spent.

- Smart Contract Capabilities
The account model offers clear advantages when it comes to enabling smart contracts.

First, the account model logic is more intuitive. Adding and subtracting balances makes it easier for developers to create transactions that require state information or involve multiple parties. A signed transaction is valid as long as the sending account has a sufficient balance to pay for the execution. Checking a balance is computationally less expensive than verifying if a transaction output is spent or unspent.

This is especially true for code controlled accounts that interact with other smart contracts. Internal transactions between contracts can be carried out in a virtual machine by adjusting the balances of the contracts. The UTXO model creates computational overhead because all spending transactions must be explicitly recorded.

Smart contracts in a UTXO model would need to include logic for choosing which outputs to use when sending assets, and logic to handle change outputs. Because the UTXO model is inherently stateless, it forces transactions to include state information, complicating the overall design.

- Other Differences
One benefit of the UTXO model is that it allows for the simpler parallelization of transactions in smart contracts. Multiple UTXOs used in different transactions can be processed at the same time since they all refer to independent inputs.

In the account model, the result of a transaction depends on the input state. Executing transactions in parallel must be handled carefully. Generally, transactions affecting the same account should be executed sequentially.

A key takeaway is that the UTXO model is better when dealing with simple transactions. The account model is beneficial when dealing with more complex logic. Hence a popular trend with current smart contract platforms is using a hybrid model where the UTXO model is used for balances, and the account model is used for smart contracts.

- Summary
Most blockchains use the UTXO model for accounting. There are a few exceptions, such as Ethereum, which actually uses an account model. The output of a transaction addressed to you is what you will use as an input to create an outgoing transaction.

When people ask what a ZEN or Bitcoin actually is, a UTXO would be the accurate answer. An unspent transaction output or UTXO that you can unlock with your private key IS your coin. There is no abstraction on top of this.

We started by pointing out the similarities between the UTXO and the account model. The blockchain can be considered a state machine independently of the accounting scheme used. In both cases, transactions trigger state transitions in batches - with each new block added to the blockchain.

In the UTXO model, the movement of assets is recorded in the form of a directed acyclic graph made of transaction outputs. New outputs are added with each additional block. In the account model, balances are stored as a global state of accounts, kept by each node, and updated with every block. This is similar to a database.

Transactions in the UTXO model are larger in size and place more burden on the user and their wallet. The UTXO model is a verification model, whereas the account model is a computational model.

Account-based systems offer storage benefits because the account’s state and transactions are smaller. The UTXO is more efficient at simplifying scaling solutions like state and payment channel constructions, as well a sharding.

Both models have pros and cons regarding privacy. For example, the account model makes it easier to link transactions to a single user, but also offers a higher degree of fungibility.

The account model offers clear advantages in regard to smart contracts. Many new smart contract platforms use hybrid models where UTXOs are used for balances and accounts are used for the contracts.

In the end, it depends on the use case, which model is better suited for the job. You can shoehorn most applications into one or the other balance model. The question is if you should do this, and why you would want to do this in the first place.

## The benefits of the UTXO Model

- Scalability — Since it is possible to process multiple UTXOs at the same time, it enables parallel transactions and encourages scalability innovation.
- Privacy — Even Bitcoin is not a completely anonymous system, but UTXO provides a higher level of privacy, as long as the users use new addresses for each transaction. If there is a need for enhanced privacy, more complex schemes, such as ring signatures, can be considered.

## The benefits of the Account/Balance Model

- Simplicity — Ethereum opted for a more intuitive model for the benefit of developers of complex smart contracts, especially those that require state information or involve multiple parties. An example is a smart contract that keeps track of states to perform different tasks based on them. UTXO’s stateless model would force transactions to include state information, and this unnecessarily complicates the design of the contracts.
- Efficiency — In addition to simplicity, the Account/Balance Model is more efficient, as each transaction only needs to validate that the sending account has enough balance to pay for the transaction.

One drawback for the Account/Balance Model is the exposure to double spending attacks. An incrementing nonce can be implemented to counteract this type of attack. In Ethereum, every account has a public viewable nonce and every time a transaction is made, the nonce is increased by one. This can prevent the same transaction being submitted more than once. (Note, this nonce is different from the Ethereum proof of work nonce, which is a random value.)
