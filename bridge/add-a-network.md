# Add nume network
This tutorial assumes you have already downloaded a Web3 wallet like MetaMask. You'll also need a chain's native currency to transact. If you're using a testnet, you can get some from a [faucet](https://faucet.polygon.technology/). If you're using a mainnet, you'll need to buy some from an exchange.

To start using the Nume bridge, you need to add the desired chain's RPC endpoint to your wallet. Here, we provide an example for doing this using the MetaMask wallet. You need to first click on the MetaMask extension on your browser, click MetaMask's network selector dropdown, and then click the Add Network button. Click "Add a network manually" and then provide the information corresponding the the Nume chain you want to connect to:

![Add network](../images/bridge/mm-add-network.png)

![Add network form](../images/bridge/mm-add-network-form.png)

**Nume testnet** :
- Network Name: Nume Testnet
- New RPC URL: https://rpc.numecrypto.com
- Chain ID: 7101
- Currency Symbol: NDAI
- Block Explorer URL: https://dev.explorer.numecrypto.com

**Nume testnet tokens** :
- WMATIC: ```0x8b58a817770AC1424931396CEc4969d2032CbB46``` ( 18 decimals ) import as ERC20
- DAI: ```0x828f7CECA102De66a6Ed4F4B6abEe0bd1bD4f9Dc``` ( 18 decimals ) native
- USDC: ```0xB6730c9ECC72509Ef46e81DF75c002C841C77418``` ( 6 decimals ) import as ERC20
- USDT: ```0xE32fb8a4BfDDfE9B01C2310439Bc00e5392A09d4``` ( 6 decimals ) import as ERC20
- WBTC: ```0xE096C6C74228c764edf3553df1E1954b7cD00542``` ( 8 decimals ) import as ERC20
- ETH: ```0x1111111111111111111111111111111111111111``` ( 18 decimals ) import as ERC20

<!-- **Nume Polygon mainnet** :
- Network Name: Nume
- New RPC URL: https://rpc.numecrypto.com
- Chain ID: 711
- Currency Symbol: MATIC
- Block Explorer URL: https://explorer.numecrypto.com -->
