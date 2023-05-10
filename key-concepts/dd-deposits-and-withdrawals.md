# Deep dive into deposits and withdrawals

> **ON THIS PAGE, WE COVER:** 
> - What are deposits and withdrawals?
> - How do deposits and withdrawals work on Nume and what assets can be deposited and withdrawn?
> - What are trustless withdrawals?
> - What is a mass exit scenario?

Users may want to transfer assets between L1 and L2, depending on the layer on which they would like to transact with them. This allows them to take advantage of the cheaper transaction fees on L2 for actions such as buying or selling NFTs, and they can withdraw them to L1 anytime they decide they want to transact on that layer instead.

### Terminology
- **Deposits** - transferring an asset from L1 to L2 (depositing to L2)
- **Withdrawal** - transferring an asset from L2 to L1 (withdrawing to L1)
- **Bridging** - another term for transferring assets between different layers

### ABI
- The Deposit ABI for the nume contract can be found [here]()
- The Withdrawal ABI for the nume contract can be found [here]()

# Deposits

Here's what happens under the hood when a deposit is made on Nume:
- User transfers the Token / MATIC from L1 to the Nume contract on L1
- The transfer function emits and event which is read by numes offchain and an asset identifier is created that represents the asset on L2, so that it can be utilized and transacted with on nume.

Sample code for depositing ERC20 to L2
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
  chainId: L1_CHAIN_ID,
}, USER_PRIVATE_KEY)
await web3.eth.sendSignedTransaction(signedTx.rawTransaction)
```

# Withdrawal
There are 2 kinds of withdrawal supported by nume
- Trusted withdrawal
- Trustless withdrawal

Here's what happens under the hood when a **trusted withdrawal** is made on Nume:
- User creates a withdrawal request on nume which will be processed in the next settlement 
- When the new settlement root is signed off all the withdrawal requests will be processed and the user will receive the asset on L1

Sample code for submitting a trusted withdrawal request

Here's what happens under the hood when a **trustless withdrawal** is made on Nume:
- User submits a withdrawal request to the L1 nume contract directly by providing his proof of ownership of the asset on L2 and 0.005 MATIC as stake.
- The nume contract on L1 verifies the proof and processes the withdrawal request. If the proof is invalid the withdrawal request is rejected.
- When the new settlement root is signed off all the withdrawal requests will be processed and the user will receive the asset on L1 and the stake amount will be returned to the user.

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
    chainId: L1_CHAIN_ID,
}, USER_PRIVATE_KEY)
await web3.eth.sendSignedTransaction(signedTx.rawTransaction)
```


?> Multiple withdrawals from L2 will be combined into one L1 transaction due to the way the bridge contract works.

# Mass exit scenario
In the event of a mass exit scenario, users can withdraw their assets from L2 to L1 without having to wait for the next settlement. This is done by submitting a withdrawal request directly to the L1 nume contract. The nume contract on L1 verifies the proof and processes the withdrawal request. If the proof is invalid the withdrawal request is rejected.
