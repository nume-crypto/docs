# NFT trades


## List NFT 

Endpoint : `POST /marketplace/list-nft`

**Request**
```sh
curl --location 'https://api.protocol.numecrypto.com/v2/marketplace/list-nft' \
--header 'Content-Type: application/json' \
--data ' {
    "user": "0xCcFf350Ef46B85228d6650a802107e58BF6A32Ab",
    "nftContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
    "nftTokenId": "18",
    "currency": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
    "amount": "2",
    "nonce": 9,
    "signature": "0x9abd891e519d84c99c3aea0521f35b2971f101a34889698d39f363972b5907907fba5b373a54ac3108e0f9752584d8668598f6c89bb3f67ecf6f44555975275a1b"
}'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| user          | string      | Address for the listing user |
| nftContractAddress | string | Address of the NFT contract |
| nftTokenId | string | Token ID of the NFT |
| currency | string | Chosen currency for NFT sale |
| amount | string | Price for the NFT in token value |
| nonce | number | Nonce of the listing user |
| signature | string | Signature of the above parameters |

**Example response:**

```json
{
    "message": {
        "Nfts": [
            {
                "OrderId": "0c27ecb1-0551-461c-87ae-e38506bec225",
                "FromUser": "0xccff350ef46b85228d6650a802107e58bf6a32ab",
                "Currency": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
                "Amount": "2",
                "NftContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
                "NftTokenId": 18
            }
        ]
    },
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------

## Buy NFT

Endpoint : `POST /marketplace/buy-nft`

**Request**
```sh
curl --location 'https://api.protocol.numecrypto.com/v2/marketplace/buy-nft' \
--header 'Content-Type: application/json' \
--data '{
    "user": "0x1b34B2f706cDA183E4818D2ceaF58253CcAb3428",
    "nftContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
    "nftTokenId": "18",
    "currency": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
    "amount": "2",
    "nonce": 8,
    "signature": "0x60326c3192e2983885e2957a830a9f78ea9d5dd6c5e7080e03c83ef661f31f454c19ba6620109e9c75b45aceaad452e2d795ce05bdc765d133b2c2f6585de4a91c"
}'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| user          | string      | Address for the listing user |
| nftContractAddress | string | Address of the NFT contract |
| nftTokenId | string | Token ID of the NFT |
| currency | string | Chosen currency for NFT sale |
| amount | string | Price for the NFT in token value |
| nonce | number | Nonce of the listing user |
| signature | string | Signature of the above parameters |

**Example response:**

```json
{
    "message": "success",
    "statusCode": 200
}
```

-------------------------------------------------------------------------------------------------------
