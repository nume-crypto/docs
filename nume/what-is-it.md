# What is it?

Nume is a gas abstracted, scalable and secure web3 payments protocol with primitives tailored for commerce. Nume chose to build on zkEVM because it is the most scalable EVM-compatible infrastructure platform on Ethereum. The Nume Protocol will launch as a Layer-3 on Polygon zkEVM.

Nume is a platform that provides:

- low-cost scaling solution for crypto asset transfers deployed as a Layer 3 on Polygon zkEVM which settles on the most secure and decentralized layer 1 - Ethereum
- APIs and developer tools aimed at making the development of web3 commerce applications hassle-free

## Designed on First Principles

Nume is a high-scale trustless asset transfer protocol. With Optimistic rollups(ORs), transactions are inexpensive but settlements have delayed finality due to its fraud proof mechanism. Zk-rollups have instant settlement finality but are expensive due to off-chain computation resources (required for the zk proof generation) and on-chain data commitment (required to guarantee data availability).

Nume provides the same security guarantees as OR/ZK systems as a validity proof system that is neither zk-based nor commits data on-chain. Hence Nume’s costs are much lower than theirs, affording for monetization strategies that is entirely gas-abstracted. Note, however, that the Nume protocol is not EVM/smart-contract compatible. We are deployed as a Layer 3 on Polygon zkEVM which allows us to tap into the network efforts of a scalable robust EVM-compatible platform while driving the cost down for asset transfers even further.

Key features of the Nume protocol::

1. **Trustless Security**
   - Nume does not make any trust assumptions on top of Polygon zkEVM. If you trust Polygon zkEVM, you can trust Nume.
2. **Data Availability**
   - Every user is revealed sufficient information about each settlement to be able to withdraw their funds trustlessly and directly from the contract at any time.
3. **Non-custodial**
   - The Nume Protocol is non-custodial and guarantees that a settlement with unauthorized changes to users’ balances will not succeed on-chain.
4. **Instant Confirmation**
   - No blockchain delays, payments are confirmed instantly on Nume. Close the loop for your customers.
5. **Decentralized Governance**
   - The protocol is governed by validators. Any changes to the Nume off chain state verification algorithm requires validators’ signature.


## EVM addressability

The Nume Protocol is fully EVM-addressable and sits behind an EVM wrapper, which means your favourite Web3 wallets and domain names will just work! Please note that the Nume Protocol isn’t smart contract compatible.

## Building with Nume

Nume provides the key functionality you’ll need to build web3 payments, token-gated commerce, web3 games or NFT applications without having to deploy your own complicated smart contracts. There is no gas associated with any of the actions. To understand how fees work in Nume network please refer to [fees](nume/fees.md) section.

1. **Facilitate user transactions**
   These enable users to do things that update state on the blockchain. These transactions include:

- Minting NFTs
- Transferring assets to other users
- Bridging assets to nume (ie. ERC20 tokens)
- Buying and selling assets

2. Retrieve data about current state and historical transactions

- Asset data : Details about non-fungible tokens on Nume, like metadata, image URL, current owner, etc.
- Order data : Details about orders, like sale price, sale period, etc.
- User data : Details about users, like the types of tokens they own and the balance of each token.
