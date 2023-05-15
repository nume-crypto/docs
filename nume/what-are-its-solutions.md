# What are its soultions?

"Layer 2" is a term used to describe mechanisms that process batches of transactions independently of layer 1 and only periodically reports them to the main chain. This decreases the total number of transactions that have to be validated on layer 1. Layer 2s are also known as "execution layers" or "rollups".
With Optimistic rollups(ORs), transactions are inexpensive but users need to wait 2 weeks to withdraw funds. Zk-rollups enable quick exit but are computationally expensive. Nume achieves costs lower than ORs while enabling ZK-like fast liquidity exit. Our protocol is based on a validity-proof system that is not a zk-rollup. 

## Benefits of building on layer 2 vs. layer 1
- **No gas fees** Transactions on layer 2 are free. This means that users can interact with your application without having to pay gas fees.
- **Limitless Scalability** Our protocol is built to support massive scale. If existing rails have not met your scaling needs, look no further. 
- **Instant Confirmation** No blockchain delays, payments are confirmed instantly on Nume. Close the loop for your customers.
- **Fast Liquidity** Transactions are settled every thirty minutes on ethereum and can be withdrawn anytime after. Access your liquidity soon after a payment is made.
- **Micropayments** Nume high scale and gas-agnostic monetization model enables you to accept one-off or streaming micropayments with a few lines of code today.

## EVM addressability
The Nume Protocol is fully EVM-addressable and sits behind an EVM wrapper, which means your favourite Web3 wallets and domain names will just work! Most of our delightful features though can only be accessed by wallets that have chosen to support a dedicated integration.

## What you can build on it?
Nume allows you to create applications on layer 2 by interacting with its API and developer tools. It provides the key functionality you'll need to build web3 games or NFT applications without having to deploy your own complicated smart contracts.

1. Facilitate user transactions
These enable users to do things that update state on the blockchain. These transactions include:

- Minting NFTs
- Transferring assets to other users
- Depositing assets to L2 (ie. ERC20 tokens)
- Buying and selling assets

2. Retrieve data about current state and historical transactions
- Asset data : Details about non-fungible tokens on Nume, like metadata, image URL, current owner, etc.
- Order data : Details about orders, like sale price, sale period, etc.
- User data : Details about users, like the types of tokens they own and the balance of each token.
