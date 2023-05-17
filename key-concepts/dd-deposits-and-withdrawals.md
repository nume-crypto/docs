# Deep dive into deposits and withdrawals

> **ON THIS PAGE, WE COVER:** 
> - What are deposits and withdrawals?
> - How do deposits and withdrawals work on Nume and what assets can be deposited and withdrawn?
> - What are trustless withdrawals?
> - What is a mass exit scenario?

Users may want to transfer assets between Nume and zkEVM, depending on the layer on which they would like to transact with them. This allows them to take advantage of the cheaper transaction fees on Nume for actions such as buying or selling NFTs, and they can withdraw them to zkEVM anytime they decide they want to transact on that layer instead.

### Terminology
- **Deposits** - transferring an asset from Nume to zkEVM (depositing to Nume)
- **Withdrawal** - transferring an asset from Nume to zkEVM (withdrawing to zkEVM)
- **Bridging** - another term for transferring assets between different layers

### ABI
- The Deposit ABI for the nume contract can be found [here](https://abis.s3.amazonaws.com/deposit_facet.abi)
- The Withdrawal ABI for the nume contract can be found [here](https://abis.s3.amazonaws.com/withdrawal_facet.abi)

# Deposits

Here's what happens under the hood when a deposit is made on Nume:
- User transfers the Token / MATIC from zkEVM to the Nume contract on zkEVM
- The transfer function emits and event which is read by Nume's offchain and an asset identifier is created that represents the asset, so that it can be utilized and transacted with on nume.

Sample code for depositing ERC20
```js
await erc20Contract.methods.approve(NUME_CONTRACT_ADDRESS, TOKEN_VALUE).send({
    from: USER_ADDRESS,
    gas: web3.utils.toHex(200000),
    gasPrice: web3.utils.toHex(200),
})
const tx = nume_contract.methods.depositERC20(USER_ADDRESS, CONTRACT_ADDRESS, TOKEN_VALUE)
const data = tx.encodeABI()
const signedTx = await web3.eth.accounts.signTransaction({
  to: NUME_CONTRACT_ADDRESS,
  data,
  gas: web3.utils.toHex(200000),
  gasPrice: web3.utils.toHex(200),
  chainId: CHAIN_ID,
}, USER_PRIVATE_KEY)
await web3.eth.sendSignedTransaction(signedTx.rawTransaction)
```

# Withdrawal
There are 2 kinds of withdrawal supported by nume
- Trusted withdrawal
- Trustless withdrawal

Here's what happens under the hood when a **trusted withdrawal** is made on Nume:
- User creates a withdrawal request on nume which will be processed in the next settlement 
- When the new settlement root is signed off all the withdrawal requests will be processed and the user will receive the asset on zkEVM

Sample code for submitting a trusted withdrawal request

Here's what happens under the hood when a **trustless withdrawal** is made on Nume:
- User submits a withdrawal request to the zkEVM nume contract directly by providing his proof of ownership of the asset on Nume and 0.005 MATIC as stake.
- The nume contract verifies the proof and processes the withdrawal request. If the proof is invalid the withdrawal request is rejected.
- When the new settlement root is signed off all the withdrawal requests will be processed and the user will receive the asset on zkEVM and the stake amount will be returned to the user.

Sample code for submitting a trustless withdrawal request
```js
const sign = async (message, secret) => {
    const hashedMessage = ethers.utils.solidityKeccak256(['bytes'], [message])
    const arrayfiedHashedMessage = ethers.utils.arrayify(hashedMessage)
    const wallet = new ethers.Wallet(secret)
    const signature = await wallet.signMessage(arrayfiedHashedMessage)
    return signature
}

let message = USER_ADDRESS + BLOCK_NUMBER.toString(16).padStart(64, '0')
let signature = await sign( message, USER_PRIVATE_KEY)
const args = {
    user: USER_ADDRESS,
    nonce: SIGNED_NONCE,
    tokenAddress: TOKEN_ADDRESS,
    balance: TOKEN_BALANCE,
    accountsProof: ACCOUNTS_PROOF,
    accountsIndex: ACCOUNTS_INDEX,
    balancesRoot: BALANCES_ROOT,
    balancesProof: BALANCES_PROOF,
    balancesIndex: BALANCES_INDEX,
    signature
}
const tx = nume_contract.methods.submitWithdrawalRequest(args)
const data = tx.encodeABI()
const signedTx = await web3.eth.accounts.signTransaction({
    to: NUME_CONTRACT_ADDRESS,
    data,
    value: '5000000000000000',
    gas: web3.utils.toHex(200000),
    gasPrice: web3.utils.toHex(200),
    chainId: CHAIN_ID,
}, USER_PRIVATE_KEY)
await web3.eth.sendSignedTransaction(signedTx.rawTransaction)
```


?> Multiple withdrawals from Nume will be combined into one zkEVM transaction due to the way the bridge contract works.

# Mass exit scenario
In the event of a mass exit scenario, users can withdraw their assets from Nume to zkEVM without having to wait for the next settlement. This is done by submitting a withdrawal request directly to the zkEVM nume contract. The nume contract on zkEVM verifies the proof and processes the withdrawal request. If the proof is invalid the withdrawal request is rejected.
