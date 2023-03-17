# What is Chainlink Automation?

*lily@gmail.com*

[Chainlink Automation](https://chain.link/automation) uses a decentralized network to monitor your automation logic securely and cost-efficiently off-chain, and then initiate an on-chain transaction to execute the smart contract function when predefined conditions are met.

In Chainlink Automation the transaction fee is paid by [LINK](https://etherscan.io/token/0x514910771AF9Ca656af840dff83E8264EcF986CA). You can find the link fee calculation [here](https://docs.chain.link/chainlink-automation/automation-economics/)

## Supported Chains

- Ethereum
- BNB Chain
- Polygon
- Avalanche
- Fantom
- Arbitrum

## Core Products of Automation

### Time-based Automation

Implement by Time-based trigger that executes your function according to a time schedule. This feature is also called the Job Scheduler and it is a throwback to the Ethereum Alarm Clock.

[Time-based Automation guide](https://docs.chain.link/chainlink-automation/job-scheduler/)

### Custom Logic Automation

Implement by custom logic trigger that provides custom solidity logic that Automation Nodes evaluate (off-chain) to determine when to execute your function on-chain. The contract must meet the requirements to be compatible with the AutomationCompatibleInterface contract. 

[Custom Logic Automation guide](https://docs.chain.link/chainlink-automation/register-upkeep/)

[Create Compatible Contracts guide](https://docs.chain.link/chainlink-automation/compatible-contracts/)

[Example Contract](https://docs.chain.link/chainlink-automation/utility-contracts/)
