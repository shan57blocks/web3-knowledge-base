# What is Hardhat?

*lily@57blocks.com*

[Hardhat](https://hardhat.org/) is a development environment for Ethereum software. It consists of different components for editing, compiling, debugging and deploying your smart contracts and dApps, all of which work together to create a complete development environment.

## Install Hardhat

Hardhat is used through a local installation in your project. This way your environment will be reproducible, and you will avoid future version conflicts.

- `npm install --save-dev hardhat`
- `yarn add --dev hardhat`

## Core Tools of Hardhat

### Hardhat Runner

[Hardhat Runner](https://hardhat.org/hardhat-runner/docs/getting-started#overview) is the main component you interact with when using Hardhat. It's a flexible and extensible task runner that helps you manage and automate the recurring tasks inherent to developing smart contracts and dApps.

Hardhat Runner is designed around the concepts of tasks and plugins. Every time you're running Hardhat from the command-line, you're running a task.Plugins are the backbone of Hardhat, and they're built using the same config API that you use in your Hardhat configuration. You can extend Hardhat's functionality with the plugins list [here](https://hardhat.org/hardhat-runner/plugins).

#### What can we do using Hardhat Runner?

- [Setting up a Hardhat project](https://hardhat.org/hardhat-runner/docs/guides/project-setup)
- [Compiling contracts](https://hardhat.org/hardhat-runner/docs/guides/compile-contracts)
- [Testing contracts](https://hardhat.org/hardhat-runner/docs/guides/test-contracts)
- [Deploying contracts](https://hardhat.org/hardhat-runner/docs/guides/deploying)
- [verifying contracts](https://hardhat.org/hardhat-runner/docs/guides/verifying)
- [Writing tasks and scripts](https://hardhat.org/hardhat-runner/docs/guides/tasks-and-scripts)
- [Console](https://hardhat.org/hardhat-runner/docs/guides/hardhat-console)
- [Create own task](https://hardhat.org/hardhat-runner/docs/advanced/create-task)
- [Build own plugins](https://hardhat.org/hardhat-runner/docs/advanced/building-plugins)
- [Flattening your contracts](https://hardhat.org/hardhat-runner/docs/advanced/flattening)

### Hardhat Network

[Hardhat Network](https://hardhat.org/hardhat-network/docs/overview) is a local Ethereum network node designed for development. It allows you to deploy your contracts, run your tests and debug your code, all within the confines of your local machine.

#### What can we do using Hardhat Runner?

- [Solidity stack traces](https://hardhat.org/hardhat-network/docs/overview#solidity-stack-traces)
- [Automatic error messages](https://hardhat.org/hardhat-network/docs/overview#automatic-error-messages)
- [Print logging messages in Solidity contracts](https://hardhat.org/hardhat-network/docs/overview#console.log)
- [Forking other networks](https://hardhat.org/hardhat-network/docs/guides/forking-other-networks)
- [Mining modes](https://hardhat.org/hardhat-network/docs/explanation/mining-modes)
- [Rich logging](https://hardhat.org/hardhat-network/docs/overview#logging)
- [The debug_traceTransaction method](https://hardhat.org/hardhat-network/docs/overview#the--debug_tracetransaction--method)

### Hardhat VSCode

[Hardhat for Visual Studio Code](https://hardhat.org/hardhat-vscode/docs/overview) is the official Hardhat extension that adds advanced support for Solidity to VSCode.

### Hardhat Chai Matchers

 [Hardhat Chai Matchers](https://hardhat.org/hardhat-chai-matchers/docs/overview) adds Ethereum-specific capabilities to the Chai assertion library, making your smart contract tests easy to write and read.

### Hardhat Network Helpers

 [Hardhat Network Helpers](https://hardhat.org/hardhat-network-helpers/docs/overview) provides a convenient JavaScript interface to the JSON-RPC functionality of Hardhat Network.

## Recommended Reading

[Hardhat Explained – What is Hardhat?](https://moralis.io/hardhat-explained-what-is-hardhat/)

[What Is Hardhat – A Comprehensive Guide](https://101blockchains.com/hardhat-tutorial/)


Hardhat helps developers in testing, compiling, deploying, and debugging dApps on the Ethereum blockchain. It serves a crucial role in supporting coders and developers with the management of tasks, which are important for smart contract and dApp development. You can try it follow the [official tutorial](https://hardhat.org/tutorial).

