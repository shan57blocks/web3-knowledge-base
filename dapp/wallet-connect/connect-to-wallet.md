In this post we will introduce some battlefield tested react libraries in order to connect users to MetaMask or any wallet from the frontend.

# web3-react

A simple, maximally extensible, dependency minimized framework for building modern Ethereum dApps

## Pros

1. Supports many different wallet connectors
2. Basic hooks for managing account
3. Used by Uniswap and some other popular projects

## Reference

- [Repo](https://github.com/Uniswap/web3-react)
- [Example](https://web3-react-mu.vercel.app/)

# wagmi

wagmi is a collection of React Hooks containing everything you need to start working with Ethereum. wagmi makes it easy to "Connect Wallet," display ENS and balance information, sign messages, interact with contracts, and much more — all with caching, request deduplication, and persistence.

## Pros

1. 20+ hooks for working with wallets, ENS, contracts, transactions, signing, etc.
2. Built-in wallet connectors for MetaMask, WalletConnect, Coinbase Wallet, and Injected
3. Caching, request deduplication, and persistence powered
4. Auto-refresh data on wallet, block, and network changes
5. Multicall support
6. Test suite running against forked Ethereum network
7. TypeScript ready (infer types from ABIs and EIP-712 Typed Data)
8. Extensive documentation and examples
9. Used by ENS, Foundation, SushiSwap, and more

## Reference

- [wagmi docs](https://wagmi.sh/react/getting-started)

# useDapp

Features:

1. React hooks - Uses React hooks as your primary building ingredient
2. Auto refresh - Refreshes on a new block, wallet change or network change
3. Multicall - Combines multiple blockchain calls into a single multicall

Best practices:

1. Modern stack - Employs ethers.js, multicall & waffle
2. Extendability - Extends easily with custom hooks
3. Testability - Simple integration tests for UI and blockchain

## Reference

- [useDapp docs](https://usedapp-docs.netlify.app/docs/)

# Web3Modal

Web3Modal is a versatile ui library built on top of WalletConnect and wagmi. It is designed to make complex tasks like connecting wallets, performing transactions and managing accounts easy. Built on top of latest web standards, Web3Modal can be used in any front-end environment. Check out web3modal.com for a live demo and in-depth feature list.

## Reference

- [Web3Modal docs](https://docs.walletconnect.com/2.0/web3modal/about)
