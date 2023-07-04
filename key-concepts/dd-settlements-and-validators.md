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

```js
ethers.utils.solidityKeccak256(
    ["address", "bytes32", "uint256"],
    [ethers.constants.AddressZero, BALANCES_ROOT, 0]
);
```

The balances root is a merkle root of the balances tree. The Balance leaf is a data structure that contains the following information:
- Asset address
- Balance or NFT token Id
- Metadata
- Type (ERC20 referred as 0 or ERC721 referred as 1)

```js
ethers.utils.solidityKeccak256(
    ["address", "uint256", "bytes32", "uint256"],
    [ethers.constants.AddressZero, 0, ethers.constants.HashZero, 0]
)
```

?> Every user has a unique settlement leaf and every asset they own has a unique balance leaf.

<!-- Assuming a settlement is ran every 1 hour, this will be the order of events. 

- User A has 100 MATIC 
- User B has 100 MATIC
- Settlement X (completed and notorized in the contract)
- User A deposits 100 MATIC
- User B deposits 100 MATIC
- User A transfers 50 MATIC to User B
- User A withdraws 50 MATIC
- User B withdraws 50 MATIC
- Settlement X+1 starts  -->

Settlements are run periodically, e.g. every 30 minutes. Transactions queued up in that duration (off-chain asset transfers, nft mints, trades, on-chain deposits, off-chain withdrawal requests, on-chain withdrawal requests) are all processed at the 30-minute mark. Processing these off-chain involves spinning up a Trusted Execution Environment where these transactions are verified (signature, nonce, balances) and the state transition resulting from these transactions is computed.  The new resultant state is attested by the private keys of registered validators.

In other words, validators of the Nume protocol register themselves with the smart-contract and make their encrypted private key available to Nume. The Trusted Execution Environment that runs the state transition algorithm has exclusive access to the symmetric key that decrypts the validators’ private keys, and uses this at each run to decipher their private key and sign the new root with it. This attested new state root is then submitted to the contract. The contract verifies validators’ signature on this root and updates the settlement root. Note that the code executed by the TEE is open-source (link broken) and validators exclusively give permission only to this code running inside the TEE to access their symmetric key”

<!-- ### Validators
Validator is a participant in the network who locks up MATIC tokens in the system and runs settlement function in order to help run the network. Validators stake their MATIC tokens as collateral to work for the security of the network and in exchange for their service, earn rewards.
Rewards are distributed to all stakers proportional to their stake at every checkpoint with the exception being the proposer getting an additional bonus. User reward balance gets updated in the contract which is referred to while claiming rewards.

!> At present there are no open validator slots available on the network. We will be opening up validator slots in the future. Please stay tuned for updates.

Validators are represented by BLS keys and are registered in the contract. The validators are responsible for submitting the rollup change. The Aggregated signature submitted by the validators is verified by the contract and the new root is updated in the contract. In current version of our protocol all validators are required to submit the aggregated signature.  -->
