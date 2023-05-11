# Token transfers


## Create transaction

Endpoint : `POST /store-eth-transaction`

**Request**
```sh
curl --location 'https://api.protocol.numecrypto.com/v2/store-eth-transaction' \
--header 'Content-Type: application/json' \
--data '{
    "data": "0x02f8aa8202c607808083033450940b6d9ab4c80889b65a61050470cbc5523d8ce48d80b844a9059cbb000000000000000000000000c8902116932225cc2e5d21d090574a54c10dc21b00000000000000000000000000000000000000000000000000000000000001cac080a0c4815012edbf440c6288f4b4b040baa885adeb80ee22b2ba161656bfd88f3f81a05c273996dfa0872cad30c222f91c517fd95f6c497689341780a638d3e53726de"
}'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| data          | string      | Raw transaction data (if from and to address is same then its considered as a withdrawal request) |

**Example response:**

```json
{
    "message": { 
        "From": "0xCcFf350Ef46B85228d6650a802107e58BF6A32Ab",
        "To": "0xc8902116932225CC2e5D21d090574A54C10DC21b",
        "TokenAddress": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
        "Amount": "458",
        "Nonce": 7,
        "TxHash": "0xa1a6ba3cddc5d2d9f6423383cee4a252fbc12e7d52c469c2c71ac6029a6d3d4f",
        "Signature": "c4815012edbf440c6288f4b4b040baa885adeb80ee22b2ba161656bfd88f3f815c273996dfa0872cad30c222f91c517fd95f6c497689341780a638d3e53726de00",
        "PublicKey": "047e6059af1164d58e6fe212282286236b6c247dcb7b8817fe35bc8dd7e8cc0e2c65e70aa0cc900a601d43b97fd9ba78a25e9293c91fd2092b5d7a8e5544bbf065"
    },
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------

## Create NFT transaction

Endpoint : `POST /store-eth-nft-transaction`

**Request**
```sh
curl --location 'https://api.protocol.numecrypto.com/v2/store-eth-nft-transaction' \
--header 'Content-Type: application/json' \
--data '{
    "data": "0x02f8ca8202c606808083033450946d9e72d1336e3592f5e4844b9e18e484fc4cf34480b86423b872dd00000000000000000000000046714661eecb6f07065dcb4bf3d9b772dcefa63a0000000000000000000000001b34b2f706cda183e4818d2ceaf58253ccab34280000000000000000000000000000000000000000000000000000000000000012c001a02f4db2ab53fe1f8fdeda2e07094fec25455a3732e7b9eec663286a09897dae5aa00d67b2dde01a22c24c441823373a2d846b7de30f628d77208ea6842d1d2d2bae"
}'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| data          | string      | Raw transaction data (if from and to address is same then its considered as a withdrawal request) |

**Example response:**

```json
{
    "message" : {
        "From": "0x46714661eECB6F07065DCb4BF3D9b772dcefa63a",
        "To": "0x1b34B2f706cDA183E4818D2ceaF58253CcAb3428",
        "NftContractAddress": "0x6D9E72D1336e3592F5E4844B9e18E484fC4cf344",
        "NftTokenId": 18,
        "Nonce": 6,
        "TxHash": "0xa0da7b21343d0ffbc8a1ef9a4046732b36ad9328b63feb07f734481cc9321e22",
        "Signature": "2f4db2ab53fe1f8fdeda2e07094fec25455a3732e7b9eec663286a09897dae5a0d67b2dde01a22c24c441823373a2d846b7de30f628d77208ea6842d1d2d2bae01",
        "PublicKey": "04edc02e29f279a53d91a61e6918ec17ce7df07dc83d4a0de952135239014fef3cf1a343dd8b5b79546e492deab691c2dc294cb8ef70859e50a688b77226da268e"
    }, 
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------

### Fetch transaction data

Endpoint : `GET /transaction/:txHash`

```sh
curl --location 'https://api.protocol.numecrypto.com/v2/transaction/0xa1a6ba3cddc5d2d9f6423383cee4a252fbc12e7d52c469c2c71ac6029a6d3d4f'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| txHash          | string      | Transaction hash |

**Example response:**

```json
{
    "message": {
        "Hash": "0xa1a6ba3cddc5d2d9f6423383cee4a252fbc12e7d52c469c2c71ac6029a6d3d4f",
        "From": "0xccff350ef46b85228d6650a802107e58bf6a32ab",
        "To": "0xc8902116932225cc2e5d21d090574a54c10dc21b",
        "CurrencyOrNftContract": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
        "CurrencyIdOrNftId": 3,
        "AmountOrNftTokenId": "458",
        "Status": "SUCCESS",
        "Nonce": 7,
        "Type": "transfer",
        "CreatedAt": "2023-05-12T00:06:24.388525+05:30"
    },
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------
