# Deep dive into asset transfers

> **ON THIS PAGE, WE COVER:**
>
> - What are the assets supported?
> - How to transfer an asset from 1 user to another?
> - Why is transfers on nume superior?

ERC20 and ERC721 are both Ethereum-based token standards. Nume supports various ERC20 tokens and ERC721 tokens.

ERC20 tokens are fungible tokens, meaning that each token is identical and interchangeable with any other token of the same type. They are commonly used for cryptocurrencies, utility tokens, and asset tokens.

ERC721 tokens are non-fungible tokens, meaning that each token is unique and not interchangeable with any other token. They are commonly used for digital assets such as collectibles, game items, and real estate.

# ERC20 tokens supported on Nume

- MATIC
- ETH
- WBTC
- USDC
- USDT
- DAI

Asset transfers refer to the process of transferring ownership of digital assets from one address to another. Asset transfers can occur for a variety of reasons, such as buying or selling assets, gifting them to others, or moving them to a different address. When someone wants to transfer an asset, they initiate a transaction on Nume. The transaction typically includes information about the asset being transferred, such as its name, type(ERC20 or ERC721), and quantity, as well as the addresses of the sender and recipient.

# ERC20 token transfer

```js
const ERC20TokenContract = contract({
  abi: ERC20TokenContractABI,
});
const ERC20TokenAddress = "";
async function transferERC20() {
  const tokenContract = await ERC20TokenContract.at(ERC20TokenAddress);
  const decimals = await tokenContract.decimals();
  const amount = 10; // replace with the amount of tokens you want to transfer
  const value = amount * 10 ** decimals;

  const gasPrice = await web3.eth.getGasPrice();
  const gasLimit = 21000;
  const tx = await tokenContract.transfer(recipientAddress, value, {
    from: senderAddress,
    gasPrice: gasPrice,
    gas: gasLimit,
  });

  console.log(`Transaction hash: ${tx.tx}`);
}

transferERC20();
```

# ERC721 token transfer

```js
const gasPrice = await web3.eth.getGasPrice();
const gasLimit = 300000; // adjust gas limit as needed
const transferOptions = {
  from: senderAddress,
  gasPrice: gasPrice,
  gas: gasLimit,
};

const transferMethod = contract.methods.transferFrom(
  senderAddress,
  recipientAddress,
  tokenId
);

transferMethod
  .send(transferOptions)
  .on("transactionHash", (hash) => {
    console.log(`Transaction hash: ${hash}`);
  })
  .on("receipt", (receipt) => {
    console.log(`Transaction receipt: ${receipt}`);
  })
  .on("error", (error) => {
    console.error(`Error: ${error.message}`);
  });
```

# Why you need to use Nume for asset transfer

- Instant payment confirmation
- Zero gas fees
