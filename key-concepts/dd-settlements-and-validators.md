# Deep dive into settlements and validators

> **ON THIS PAGE, WE COVER:** 
> - What is a settlement?
> - Who are validators and what is their role in settlement?
> - Where does the settlement happen?
> - What happens in a settlement?

# Settlement
Before going into settlements let's understand what a rollup is. A rollup is a scaling solution that allows for off-chain processing of crypto transactions and only commits the final state to the main chain. This enables a large number of transactions to be processed in a single “settlement” transaction on the main chain.

### Settlement tree and leaf structure
Settlement leaf is a data structure that contains the following information:
- Address
- Balances root
- Last signed nonce
- Optimized lister nonce hash
- Subscribed settlement number

```js
const leafHash = (user, balanceRoot, nonce, listerNonce, subNum) => {
    let types = []
    let values = []
    listerNonce.forEach((nonce) => {
        types.push('uint256')
        values.push(nonce)
    })
    let listerNonceHash = ethers.utils.solidityKeccak256(types, values)
    if (listerNonce.length === 0) listerNonceHash = ethers.utils.formatBytes32String('')
    return ethers.utils.solidityKeccak256(
        ['address', 'bytes32', 'uint256', 'bytes32', 'uint256'],
        [user, balanceRoot, nonce, listerNonceHash, subNum],
    )
}
```

The balances root is a merkle root of the balances tree. The Balance leaf is a data structure that contains the following information:
- Asset address
- Balance or NFT token Id
- Type (ERC20 referred as 0 or ERC721 referred as 1)
- L2Minted (0 or 1)

```js
ethers.utils.solidityKeccak256(
    ["address", "uint256", "uint256", "uint256"],
    [ethers.constants.AddressZero, 0, 0, 0]
)
```

?> Every user has a unique settlement leaf and every asset they own has a unique balance leaf.

Settlements are run periodically, e.g. every 30 minutes. Transactions queued up in that duration (off-chain asset transfers, nft mints, trades, on-chain deposits, off-chain withdrawal requests, on-chain withdrawal requests) are all processed at the 30-minute mark. Processing these off-chain involves spinning up a Trusted Execution Environment where these transactions are verified (signature, nonce, balances) and the state transition resulting from these transactions is computed.  The new resultant state is attested by the settlement verification address (SVA).  The Nume contract verifies the signature and updates the state. The new state is now the current state of the Nume protocol.

Validators of the Nume protocol collectively agree to the SVA address which is generated and handled by intel SGX and publish it to the Nume contract. Only the TEE has the permission to sign with the SVA address.


## How SVA is handled?
Nume enclave is a trusted execution environment that runs on a SGX enabled machine and the code can be found in [here](https://github.com/nume-crypto/nume-enclave-p2p).
Every time there is a code change caused by a feature addiotion or a bug fix the following steps happen 
- A new enclave is built in a SGX enabled machine.
- The enclave generates a private key and seals it with the unique id and returns the address (SVA).
- Nume creates a proposal for change on tally and the validators vote on it. [Nume DAO](https://www.tally.xyz/gov/Nume-Crypto-prod) is used for governance.
- The proposal lasts for 14 days, the community can go through the chagnes and if not in favour can exit the network. They can also verify the enclaves unique id by reporducing the build by following the steps in the [sgx uniqueid verification docs](https://www.notion.so/numecrypto/Sgx-unqiueid-verification-5ff9223339774b428f6f5f6e9b8a483d)
- Once the proposal is passed the new SVA is updated in the Nume contract.
