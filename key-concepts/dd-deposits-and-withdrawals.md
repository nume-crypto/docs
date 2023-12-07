# Deep dive into deposits and withdrawals

> **ON THIS PAGE, WE COVER:** 
> - What are deposits and withdrawals?
> - How do deposits and withdrawals work on Nume and what assets can be deposited and withdrawn?
> - What are trustless withdrawals?
> - What is a mass exit scenario?

?> The Nume Protocol will launch as a Layer-3 on Polygon zkEVM.

Users can transfer assets between Nume and Polygon zkEVM, depending on the desired transaction layer. This enables them to benefit from lower transaction fees on Nume for actions like buying or selling NFTs, with the flexibility to withdraw to Polygon zkEVM when transacting on that layer.

### Terminology
- **Deposits** - Deposits involve transferring assets from Polygon zkEVM to Nume (adding funds to Nume).
- **Withdrawal** - Withdrawals involve transferring assets from Nume to Polygon zkEVM (withdrawing from Nume).
- **Bridging** - Bridging refers to transferring assets between different layers.

### ABI (Application Binary Interface)
- The ERC20 Deposit ABI for the nume contract can be found [here](https://nume-public.s3.amazonaws.com/abis/deposit_facet.abi)
- The NFT ABI for the nume contract can be found [here](https://nume-public.s3.amazonaws.com/abis/nft_deposit_facet.abi)
- The Withdrawal ABI for the nume contract can be found [here](https://nume-public.s3.amazonaws.com/abis/withdrawal_facet.abi)

# Deposits

Here's what happens under the hood when a deposit is made on Nume:
- User transfers the Token from Polygon zkEVM to the Nume contract on Polygon zkEVM
- The transfer function emits an event which is read by Nume's server and an asset identifier is created, so that it can be utilized and transacted with on nume.

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
?> Deposits are queued and processed in the next settlement.

# Withdrawal
There are 2 kinds of withdrawal supported by nume
- Trusted withdrawal
- Trustless withdrawal

Here's what happens under the hood when a **trusted withdrawal** is made on Nume:
- User creates a withdrawal request on nume which will be processed in the next settlement 
- When the new settlement root is signed off all the withdrawal requests will be processed and the user will receive the asset on Polygon zkEVM

Guidelines for submitting a [trusted withdrawal request](./guides/token-transfer?id=create-transaction)

Here's what happens under the hood when a **trustless withdrawal** is made on Nume:
- User submits a withdrawal request to the Polygon zkEVM nume contract directly by providing his proof of ownership of the asset on Nume and 0.01 ETH as stake.
- The nume contract verifies the proof and processes the withdrawal request. If the proof is invalid the withdrawal request is rejected.
- When the new settlement root is signed off all the withdrawal requests will be processed and the user will receive the asset on Polygon zkEVM and the stake amount will be returned to the user.

Sample code for submitting a trustless withdrawal request
```js
const sign = async (message, secret) => {
    const hashedMessage = ethers.utils.solidityKeccak256(['bytes'], [message])
    const arrayfiedHashedMessage = ethers.utils.arrayify(hashedMessage)
    const wallet = new ethers.Wallet(secret)
    const signature = await wallet.signMessage(arrayfiedHashedMessage)
    return signature
}

const getOptimizedNonce = (usedListerNonce) => {
    let optimizedUsedListerNonce = []
    usedListerNonce.sort((a, b) => a - b)
    let lastOptimizedNonce = 0

    for (let i = 0; i < usedListerNonce.length; i++) {
    let nonce = usedListerNonce[i]
    if (i + 1 === nonce) {
        lastOptimizedNonce = nonce
        continue
    } else {
        if (lastOptimizedNonce !== 0) {
        optimizedUsedListerNonce.unshift(0)
        optimizedUsedListerNonce.push(lastOptimizedNonce)
        lastOptimizedNonce = 0
        }
        optimizedUsedListerNonce.push(nonce)
    }
    }

    if (lastOptimizedNonce !== 0) {
    optimizedUsedListerNonce.unshift(0)
    optimizedUsedListerNonce.push(lastOptimizedNonce)
    lastOptimizedNonce = 0
    }
    return optimizedUsedListerNonce
}

let message = USER_ADDRESS.slice(2) + BLOCK_NUMBER.toString(16).padStart(64, '0')
let signature = await sign( message, USER_PRIVATE_KEY)
const args = {
    user: USER_ADDRESS,
    tokenAddress: TOKEN_ADDRESS,
    balanceOrTokenId: TOKEN_BALANCE/NFT_TOKEN_ID,
    isNft: true/false,
    mintedNft: true/false,
    nonce: SIGNED_NONCE,
    listerNonce: getOptimizedNonce(USER_LISTED_NONCE || []),
    accountsProof: ACCOUNTS_PROOF,
    accountsIndex: ACCOUNTS_INDEX,
    balancesRoot: BALANCES_ROOT,
    balancesProof: BALANCES_PROOF,
    balancesIndex: BALANCES_INDEX,
    signature,
    subscriptionSettlementNumber: USER_SUBSCRIPTION_NUMBER || 0,

}
const tx = nume_contract.methods.submitWithdrawalRequest(args)
const data = tx.encodeABI()
const signedTx = await web3.eth.accounts.signTransaction({
    to: NUME_CONTRACT_ADDRESS,
    data,
    value: '10000000000000000',
    gas: web3.utils.toHex(200000),
    gasPrice: web3.utils.toHex(200),
    chainId: CHAIN_ID,
}, USER_PRIVATE_KEY)
await web3.eth.sendSignedTransaction(signedTx.rawTransaction)
```


?> Multiple withdrawals from Nume will be combined into one Polygon zkEVM transaction due to the way the bridge contract works.

# Mass exit scenario
During a mass exit scenario, users can efficiently withdraw their assets from Nume to Polygon zkEVM. Users can submit a withdrawal request directly to the Polygon zkEVM Nume contract, which verifies the proof and processes the withdrawal. If the proof is invalid, the withdrawal request is rejected.

?> **Deposit and withdrawal is limited to 6 per day to prevent bad actors from overwhelming our system, but there's no limit on the amounts to withdraw or deposit.**
