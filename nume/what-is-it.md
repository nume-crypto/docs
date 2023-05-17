# What is it?

Nume is a gas abstracted, scalable and secure web3 payments protocol with primitives tailored for commerce. Nume chose to build on zkEVM because it is the most scalable EVM-compatible infrastructure  platform on Ethereum.

Nume is a platform that provides:
- low-cost scaling solution for crypto asset transfers deployed as a Layer 3 on zkEVM which settles on the most secure and decentralized layer 1 - Ethereum
- APIs and developer tools aimed at making the development of web3 commerce applications hassle-free


## Designed on First Principles
Nume is a high-scale trustless asset transfer protocol. With Optimistic rollups(ORs), transactions are inexpensive but settlements have delayed finality due to its fraud proof mechanism. Zk-rollups have instant settlement finality but are expensive due to off-chain computation resources (required for the zk proof generation) and on-chain data commitment (required to guarantee data availability). Nume provides the same security guarantees as OR/ZK systems as a validity proof system that is neither zk-based nor commits data on-chain. Hence Nume’s costs are much lower than theirs, affording for monetization strategies that is entirely gas-abstracted. Note, however, that the Nume protocol is not EVM/smart-contract compatible. We are deployed as a Layer 3 on zkEVM which allows us to tap into the network efforts of a scalable robust EVM-compatible platform while driving the cost down for asset transfers even further.

Key features of the Nume protocol::
- **Trustless Security** Nume does not make any trust assumptions on top of zkEVM. If you trust zkEVM, you can trust Nume. 
- **Data Availability** Every user is revealed sufficient information about each settlement to be able to withdraw their funds trustlessly and directly from the contract at any time.
- **Non-custodial** The Nume Protocol is non-custodial and guarantees that a settlement with unauthorized changes to users’ balances will not succeed on-chain.
- **Instant Confirmation** No blockchain delays, payments are confirmed instantly on Nume. Close the loop for your customers.
- **Decentralized Governance** (COMING SOON) The protocol is governed by validators. Any changes to the Nume off chain state verification algorithm requires validators’ signature.

<!-- ## Benefits of building on layer 2 vs. layer 1
- **No gas fees** Transactions on layer 2 are free. This means that users can interact with your application without having to pay gas fees.
- **Limitless Scalability** Our protocol is built to support massive scale. If existing rails have not met your scaling needs, look no further. 
- **Instant Confirmation** No blockchain delays, payments are confirmed instantly on Nume. Close the loop for your customers.
- **Fast Liquidity** Transactions are settled every thirty minutes on ethereum and can be withdrawn anytime after. Access your liquidity soon after a payment is made.
- **Micropayments** Nume high scale and gas-agnostic monetization model enables you to accept one-off or streaming micropayments with a few lines of code today. -->

## EVM addressability
The Nume Protocol is fully EVM-addressable and sits behind an EVM wrapper, which means your favourite Web3 wallets and domain names will just work! Please not how ever that Nume protocol is not smart contract compatible.

## What you can build on it?
Nume provides the key functionality you’ll need to build web3 payments, token-gated commerce, web3 games or NFT applications without having to deploy your own complicated smart contracts. There is no gas associated with any of the actions. To understand how fees work in nume network please refer to [fees](nume/fees.md) section.

1. **Facilitate user transactions**
These enable users to do things that update state on the blockchain. These transactions include:

- Minting NFTs
- Transferring assets to other users
- Depositing assets to nume (ie. ERC20 tokens)
- Buying and selling assets

2. Retrieve data about current state and historical transactions
- Asset data : Details about non-fungible tokens on Nume, like metadata, image URL, current owner, etc.
- Order data : Details about orders, like sale price, sale period, etc.
- User data : Details about users, like the types of tokens they own and the balance of each token.
