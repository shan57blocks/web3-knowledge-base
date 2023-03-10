# UTXO VS. ACCOUNT MODEL

The blockchain can be considered a state machine independently of the accounting scheme used. In both cases, transactions trigger state transitions in batches - with each new block added to the blockchain.
Below, we will compare the strengths and weaknesses of the UTXO and account model. We will start by comparing them at a high-level computational view, and then move onto scalability, privacy, smart contract capabilities, and more.

## In General

The UTXO model is a verification model.

This means users submit transactions that specify the results of the state transition, defined as new transaction outputs spendable by the receiver(s). Nodes then verify if the consumed inputs are unspent and if the signature(s) satisfy the spending conditions.

The account model, on the other hand, is a computational model.

In this model, users submit transactions instructing nodes on what state transitions should look like. The network then computes the new state based on the instructions. This method comes with specific implications regarding second layer scalability solutions like state channels and sharding.

## Comparasion

| Features          | UTXO Model   | Account Model |
| ----------------- | ------------ | ------------- |
| Conceptual | Complicated | Intuitive |
| Parrallization | Yes | No |
| Scability | enables parallel transactions and encourages scalability innovation | No |
| Memory Usage | More effecient | less effecient |
| Privacy | Higher level of privacy, harder to link transactions | Lower level of privacy |
| Sharding | Aggregating spendable transaction outputs and defining the outputs happens on the client-side, reducing the stress on the overall system | every node has to localize the sender’s and receiver’s account across different shards and edit both |
| Smart Contract Capabilities | hard to build | easy to build |

## References

<https://www.horizen.io/academy/utxo-vs-account-model/#comparing-the-utxo-and-account-model>
<https://www.youtube.com/watch?v=-xoCoZGJ9AQ>
<https://www.youtube.com/watch?v=VT2o4KCEbes>
