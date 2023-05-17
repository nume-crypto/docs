# Deep dive into asset transfers

> **ON THIS PAGE, WE COVER:**
>
> - What are the assets supported?
> - How to transfer an asset from 1 user to another?

ERC20 and ERC721 are both Ethereum-based token standards. Nume supports various ERC20 tokens and ERC721 tokens.

ERC20 tokens are fungible tokens, meaning that each token is identical and interchangeable with any other token of the same type. They are commonly used for cryptocurrencies, utility tokens, and asset tokens.

ERC721 tokens are non-fungible tokens, meaning that each token is unique and not interchangeable with any other token. They are commonly used for digital assets such as collectibles, game items, and real estate.

# ERC20 tokens currently supported on Nume

- MATIC
- ETH
- WBTC
- USDC
- USDT
- DAI

These supported tokens will be expanded upon request.
Asset transfers refer to the process of transferring ownership of digital assets from one address to another. Asset transfers can occur for a variety of reasons, such as buying or selling assets, gifting them to others, or moving them to a different address. When someone wants to transfer an asset, they initiate a transaction on Nume. The transaction typically includes information about the asset being transferred, such as its name, type(ERC20 or ERC721), and quantity, as well as the addresses of the sender and recipient.

# ERC20 token transfer

```js
const tx = {
  to: web3.utils.toHex(ERC20_CONTRACT_ADDRESS),
  gasLimit: web3.utils.toHex(0),
  maxFeePerGas: web3.utils.toHex(web3.utils.toWei('0', 'gwei')),
  maxPriorityFeePerGas: web3.utils.toHex(web3.utils.toWei('0', 'gwei')),
  value: web3.utils.toHex(web3.utils.toWei('0', 'ether')),
  nonce: web3.utils.toHex(USER_NONCE + 1),
  chainId: web3.utils.toHex(NUME_CHAIN_ID),
  accessList: [],
  type: 2,
  data:
    '0xa9059cbb' + // transfer(address,uint256)
    ethers.utils
      .solidityPack(['address', 'uint256'], [toUserAddress, tokenValue])
      .slice(2)
      .padStart(128, '0'),
}
const signedTx = await wallet.signTransaction(tx)
```
?>  Use the signedTx for making the transfer [API call](../guides/asset-transfer.md)
