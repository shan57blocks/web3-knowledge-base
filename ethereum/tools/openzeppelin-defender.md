# What is Openzeppelin Defender

*lily@57blocks.com*

[OpenZeppelin Defender](https://www.openzeppelin.com/defender) is a web-based application that allows developers to perform and automate smart contract operations in a secure way.

## Core Products of Defender

### Relay

The Defender Relay service allows you to send transactions via a regular HTTP API, and takes care of private key secure storage, transaction signing, nonce management, gas pricing estimation, and resubmissions. 

[More](https://docs.openzeppelin.com/defender/relay)


[Example - Running a Keep3r Network keeper](https://docs.openzeppelin.com/defender/guide-keep3r)

### Autotasks

The Defender Autotasks service allows you to run code snippets on a regular basis, via webhooks, or in response to a transaction. Tight integration to Relay and Sentinels, you can use Autotasks to automate regular actions by easily sending transactions or reacting to events from your contracts.

#### Use Cases

- Check your balance in contracts and sweep funds to a wallet upon reaching a threshold
- Update an on-chain oracle with information from an external API
- Monitor your contracts to verify their state or check that an off-chain data source is in-sync
- Poke your contracts to have them transition to a new state once a set of conditions is met
- Integrate with external third party services via webhooks
- Provide gasless transactions for your dapp users via meta-transactions

[More](https://docs.openzeppelin.com/defender/autotasks)


[Example - Running a Keep3r Network keeper](https://docs.openzeppelin.com/defender/guide-keep3r)

### Sentinel

The Defender Sentinel service offers 3 types of Sentinels, Contract Sentinels, Forta Sentinels and Forta Local Mode Sentinels. Contract Sentinels allow you to monitor transactions to a contract by defining conditions on events, functions, transaction parameters. Forta Sentinels allow you to monitor Forta Alerts by defining conditions on Forta Bots, contract addresses, alert IDs and severity. If a Sentinel matches a transaction or a Forta Alert based on your defined conditions it will notify you via email, slack, telegram, discord, Autotasks, and more.

#### Use Cases

- Monitor your sensitive functions like transferOwnership, pause, or upgrade
- Alert on potentially dangerous transactions on your contracts
- Respond by executing logic when key events happen
- Integrate with your existing tools through slack, telegram, discord, email or custom Autotask integration
- Know when an unexpected volume of transactions or alerts occur

[More](https://docs.openzeppelin.com/defender/sentinel)

### Admin

The Defender Admin service acts as an interface to manage your smart contract project through secure multisig contracts or timelocks.

#### Use Cases

- Upgrading a contract to a new implementation
- Tweaking a numerical parameter in your protocol that affects its behavior
- Managing an access control list for restricted operations
- Pausing your contract in the event of an emergency

[More](https://docs.openzeppelin.com/defender/admin)


[Example - How to manage roles on a TimelockController using Defender Admin](https://docs.openzeppelin.com/defender/guide-timelock-roles)

[Example - Upgrading a contract via a multisig](https://docs.openzeppelin.com/defender/guide-upgrades)


### Logging

Defender generates log trails of every potentially relevant event in the system. This includes manual actions, such as modifying an Autotask or Sentinel, as well as automated actions, such as sending a transaction or firing a notification. Logs can be optionally forwarded to Datadog or Splunk for aggregation. This is a premium feature.

#### Use Cases

- Track user actions on your team by monitoring sign ins and activity across the application
- Detect potential attacks on your infrastructure from failed sign in attempts
- Follow relayer activity to understand the transactions being sent from your accounts
- Keep an audit trail of all changes to your Autotasks, Sentinels, and Relayers

[More](https://docs.openzeppelin.com/defender/logging)

### Advisor

The Defender Advisor service contains a knowledge base of security best practices curated by the OpenZeppelin team. The best practices cover development, testing, monitoring and operations. Defender Advisor can be used as a checklist to prioritize efforts in implementing project security.

#### Use Cases

- Evaluate your security versus established best practices
- Prioritize additional best practices that you can implement
- Improve security training and awareness within your development and operations teams

[More](https://docs.openzeppelin.com/defender/advisor)


### Practice Examples

[Registering an Upkeep on Chainlink Keepers](https://docs.openzeppelin.com/defender/guide-chainlink)

[Automated Security Monitoring of Factory Clones](https://docs.openzeppelin.com/defender/guide-factory)

[How to Relay Gasless Meta-Transactions](https://docs.openzeppelin.com/defender/guide-metatx)

[Pause Guardian - Automated Incident Response Using Defender](https://docs.openzeppelin.com/defender/guide-pauseguardian)