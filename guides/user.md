# Users

Our chain uses EVM compatible addresses to identify users. This means that you can use any Ethereum wallet to interact with our chain.  Each user has a unqiue leaf in the settlements tree and every asset he owns has a leaf in the balances tree.

## Fetch user data

Endpoint : `GET /fetch-user-data/:address`

```sh
curl --location 'https://api.protocol.numecrypto.com/v2/fetch-user-data/0xccff350ef46b85228d6650a802107e58bf6a32ab'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| address         | string      | Address of the user to be fetched  |

**Example response:**

```json
{
    "message": {
        "Nonce": 6
    },
    "BalanceLeaves": [
            {
                "Type": 0,
                "CurrencyOrNftContract": "0x0000000000000000000000000000000000000000",
                "AmountOrTokenId": "0",
                "MetaData": "0x0000000000000000000000000000000000000000"
            },
    ],
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------

### Fetch user balance

Endpoint : `GET /fetch-user-balance/:address`

```sh
curl --location 'https://api.protocol.numecrypto.com/v2/fetch-user-balance/0x46714661eecb6f07065dcb4bf3d9b772dcefa63a'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| address          | string      | Address of the user to be fetched |

**Example response:**

```json
{
    "message": {
        "UserBalances": [
            {
                "CurrencyId": 6,
                "Amount": "0",
                "ContractAddress": "0x0000000000000000000000000000000000000000",
                "Abbreviation": "MATIC"
            },
            {
                "CurrencyId": 4,
                "Amount": "734630000",
                "ContractAddress": "0xE9573B8A0AF951431bcBD194E8cc3AeE654Cd723",
                "Abbreviation": "USDC"
            }
        ]
    },
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------

### Fetch user currency balance

Endpoint : `GET /fetch-user-balance/:address/:tokenAddress`

```sh
curl --location 'https://api.protocol.numecrypto.com/v2/fetch-user-balance/0x46714661eecb6f07065dcb4bf3d9b772dcefa63a/0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| address          | string      | Address of the user to be fetched |
| tokenAddress          | string      | Address of the token to be fetched |

**Example response:**

```json
{
    "message": {
        "UserBalances": {
            "CurrencyId": 4,
            "Amount": "734630000",
            "ContractAddress": "0xE9573B8A0AF951431bcBD194E8cc3AeE654Cd723",
            "Abbreviation": "USDC"
        }
    },
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------

### Fetch user proofs

Endpoint : `GET /fetch-user-balance/:address/:tokenAddress`

```sh
curl --location 'https://api.protocol.numecrypto.com/v2/fetch-user-proof/0x29f1df30dfa1f627fcfe35c24597d202cf72238f/0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| address          | string      | Address of the user to be fetched |
| tokenAddress          | string      | Address of the token to be fetched |

**Example response:**

```json
{
    "message": {
        "AccountIndex": 0,
        "AccountProof": [
            "0x5306fccd46eeea13a7b7ba988a94514277db096872995cf086250194e5d8367a",
            "0xe41866f18bc2b9502fccc217a5572755dab1f9ca439846b75c3f91f15dd9c28b",
            "0x1989cb201b9b6ba3b3a98aeaac29638c95b11fd3e2e77aa7712a8d2095bef2a4",
            "0xe97e5ec1c1266505544143852b8fd3045e1add92ddaadfb34ee38be20f2c2e7e"
        ],
        "AccountProofHelper": [
            1,
            1,
            1
        ],
        "BalancesRoot": "0x89d7e77cdef0473233ac43d43df3c7b93c6bfbbf40bdd9c007ed747383946d99",
        "BalancesProof": [
            "0xa86d54e9aab41ae5e520ff0062ff1b4cbd0b2192bb01080a058bb170d84e6457",
            "0x4b4efd86a2cec7174648fca755d3b9caf672051f139e1b37846d357f29e0d889",
            "0x2a3c055e5aad1f95e094e401d23a52dd4975291cc3ecbaef3a11c98dfdef94b8"
        ],
        "Balance": "753820000",
        "BalancesIndex": 0
    },
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------

### Fetch nft owner

Endpoint : `GET /fetch-nft-user-owner/:tokenAddress/:tokenId`

```sh
curl --location 'https://api.protocol.numecrypto.com/v2/fetch-nft-user-owner/0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344/18'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| tokenId          | uint      | Token id of the nft |
| tokenAddress          | string      | Address of the token to be fetched |

**Example response:**

```json
{
    "message": "0x46714661eecb6f07065dcb4bf3d9b772dcefa63a",
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------

### Fetch user nft balance

Endpoint : `GET /fetch-user-balance/:address`

```sh
curl --location 'https://api.protocol.numecrypto.com/v2/fetch-user-nft-balance/0x46714661eecb6f07065dcb4bf3d9b772dcefa63a'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| address          | string      | Address of the user to be fetched |

**Example response:**

```json
{
    "message": {
        "UserBalances": [
            {
                "NftContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
                "NftTokenId": 18
            }
        ]
    },
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------
