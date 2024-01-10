# Nume gas sponsoring apis

## Gas sponsor token transfer

Endpoint : `POST /sponsored-transfer`

**Request**

```sh
curl --location '{{apiUrl}}sponsored-transfer' \
--data '{
    "from": "0xCcFf350Ef46B85228d6650a802107e58BF6A32Ab",
    "to": "0x11c830B25a15E39006094377fDc409c11C002B48",
    "amount": "100",
    "nonce": 8,
    "currency": "0x8b58a817770AC1424931396CEc4969d2032CbB46",
    "sponsor": "0x1b34B2f706cDA183E4818D2ceaF58253CcAb3428",
    "sponsorSignature": "0x483e8a4b8cb5c0abc39c9fa2e57c0e741a3b8a85eadfce5a901f772d1d77f5aa69b07d2bce54597fae8fb7295e2ec836272051527dbe1c21807f3e0159765b0c1c",
    "userSignature": "0xc3e331282c5691735bf6cc2607a067129a48ea37c8d676698ec57e148964f24b11dbd72e82819df69032e10f8beaae5decd8384c2f90b50604741fec954bb8c01b"
}'
```

**Parameters:**

| Name             | Type   | Description                             |
| ---------        | ------ | --------------------------------------- |
| from             | string | address of the user                     |
| to               | string | signature signed on the message by user |
| currency         | string | currency to transfer                    |
| amount           | string | amount to transfer                      |
| nonce            | number | nonce of the user                       |
| userSignature    | number | user signature for transfer             |
| sponsor          | number | address of sponsor                      |
| sponsorSignature | number | sponsor signature for approval          |

**Signature construction:**

```js
// USER MESSAGE
const userMessage = ethers.utils.solidityKeccak256(
    ['address', 'address', 'uint256', 'address', 'uint256', 'address'],
    [from, to, amount, currency, nonce, sponsor],
)
// SPONSOR MESSAGE
const sponsorMessage = ethers.utils.solidityKeccak256(['bytes32', 'uint256'], [userMessage, fee])
```

**Example response:**

```json
{
    "message": "success",
    "statusCode": 200
}
```

---

## Gas sponsor nft transfer

Endpoint : `POST /sponsored-nft-transfer`

**Request**

```sh
curl --location '{{apiUrl}}sponsored-nft-transfer' \
--data '{
    "from": "0xc8902116932225CC2e5D21d090574A54C10DC21b",
    "to": "0x11c830B25a15E39006094377fDc409c11C002B48",
    "contractAddress": "0xc51ab950f2b93686b423b59a7e1d1ed2a1d10d4b",
    "nonce": 7,
    "tokenId": "11",
    "sponsor": "0x1b34B2f706cDA183E4818D2ceaF58253CcAb3428",
    "sponsorSignature": "0x51687421a48a732e6842146454f7bc0a23bb49edd88dc4fe508c36a157d6d1af36b8a41f0acf02e585f35aee3ed11e324f3b8ac4d1e3a57b50e822500fb87a761c",
    "userSignature": "0xc279f1388ba418001d2a22e8ce63545be8da7a7a02b92346a15aa13677a77d686e5b1de9379cb5411c5fc7284b8abd9aa89ad729e32750550b880d206f9f360a1b"
}'
```

**Parameters:**

| Name             | Type   | Description                             |
| ---------        | ------ | --------------------------------------- |
| from             | string | address of the user                     |
| to               | string | signature signed on the message by user |
| contractAddress  | string | contractAddress of nft                  |
| tokenId          | string | tokenId of nft                          |
| nonce            | number | nonce of the user                       |
| userSignature    | number | user signature for transfer             |
| sponsor          | number | address of sponsor                      |
| sponsorSignature | number | sponsor signature for approval          |

**Signature construction:**

```js
// USER MESSAGE
const userMessage = ethers.utils.solidityKeccak256(
    ['address', 'address', 'uint256', 'address', 'uint256', 'address'],
    [from, to, tokenId, contractAddress, nonce, sponsor],
)
// SPONSOR MESSAGE
const sponsorMessage = ethers.utils.solidityKeccak256(['bytes32', 'uint256'], [userMessage, fee])
```

**Example response:**

```json
{
    "message": "success",
    "statusCode": 200
}
```

---

## Gas sponsor nft mint

Endpoint : `POST /sponsored-nft-mint`

**Request**

```sh
curl --location '{{apiUrl}}sponsored-nft-mint' \
--data '{
    "mintUser": "0xc8902116932225CC2e5D21d090574A54C10DC21b",
    "contractAddress": "0xc51ab950f2b93686b423b59a7e1d1ed2a1d10d4b",
    "nonce": 7,
    "sponsor": "0x1b34B2f706cDA183E4818D2ceaF58253CcAb3428",
    "sponsorSignature": "0x6251630e538de0b0be9c69c90a216ac57072c224562e7aef6be4f958865c49d67fa6e52474619292c4388c338809a1cdc4c2de625d06801e1e45f1d64ea4d93c1c",
    "userSignature": "0xc32b5503c45f0b2c1d101cefbab9cb00340ec16a620c1ed2617cf9492c4bc4546cb083f3aa8a34644eea648bf8e45a2e6d26e753fc0068a6c4ce0bc30dfda14d1c"
}'
```

**Parameters:**

| Name             | Type   | Description                             |
| ---------        | ------ | --------------------------------------- |
| contractAddress  | string | address of the nft collection           |
| mintUser         | string | address of mint user                    |
| nonce            | number | nonce of the user                       |
| userSignature    | number | user signature for transfer             |
| sponsor          | number | address of sponsor                      |
| sponsorSignature | number | sponsor signature for approval          |

**Signature construction:**

```js
// USER MESSAGE
const userMessage = ethers.utils.solidityKeccak256(
    ['uint256', 'address', 'address', 'uint256', 'address', 'address'],
    [nonce, nftContractAddress, user, mintFee, mintFeeCurrency, sponsor],
)
// SPONSOR MESSAGE
const sponsorMessage = ethers.utils.solidityKeccak256(['bytes32', 'uint256'], [userMessage, fee])
```

**Example response:**

```json
{
    "message": {
        "ContractAddress": "0xc51ab950f2b93686b423b59a7e1d1ed2a1d10d4b",
        "MintUser": "0xc8902116932225cc2e5d21d090574a54c10dc21b",
        "NftTokenId": "16"
    },
    "statusCode": 200
  }
```

---
