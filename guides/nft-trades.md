# NFT trades

## List NFT

Endpoint : `POST /marketplace/list-nft`

**Request**

```sh
curl --location '{{apiUrl}}marketplace/list-nft' \
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

| Name               | Type   | Description                       |
| ------------------ | ------ | --------------------------------- |
| user               | string | Address for the listing user      |
| nftContractAddress | string | Address of the NFT contract       |
| nftTokenId         | string | Token ID of the NFT               |
| currency           | string | Chosen currency for NFT sale      |
| amount             | string | Price for the NFT in token value  |
| nonce              | number | Lister Nonce of the user          |
| signature          | string | Signature of the above parameters |

> Lister nonce is different from nonce that we use generally in other calls. This is specifically created to be use during NFT listings. The reason for going ahead with this approach is to facilitate NFT sales. To keep it simple when a user lists an NFT, it will be signed by the user which includes nonce, and if the user does some other transactions on Nume thereby increasing the nonce, will make the nonce that was signed during listing invalid. To avaoid this we are having a seperate nonce to track NFT listings.

**Example response:**

```json
{
  "message": {
    "Nfts": [
      {
        "OrderId": "c0ab9ec2-8d33-41e6-bb37-5b88435d3479",
        "FromUser": "0xccff350ef46b85228d6650a802107e58bf6a32ab",
        "Currency": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
        "Amount": "2",
        "NftContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
        "NftTokenId": "18"
      }
    ]
  },
  "statusCode": 200
}
```

---

## Buy NFT

Endpoint : `POST /marketplace/buy-nft`

**Request**

```sh
curl --location '{{apiUrl}}marketplace/buy-nft' \
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

| Name               | Type   | Description                       |
| ------------------ | ------ | --------------------------------- |
| user               | string | Address for the listing user      |
| nftContractAddress | string | Address of the NFT contract       |
| nftTokenId         | string | Token ID of the NFT               |
| currency           | string | Chosen currency for NFT sale      |
| amount             | string | Price for the NFT in token value  |
| nonce              | number | Nonce of the user                 |
| signature          | string | Signature of the above parameters |

**Example response:**

```json
{
  "message": "success",
  "statusCode": 200
}
```

---

## Unlist NFT

Endpoint : `POST /marketplace/unlist-nft`

**Request**

```sh
curl --location '{{apiUrl}}marketplace/unlist-nft' \
--header 'Content-Type: application/json' \
--data '{
    "user": "0x1b34B2f706cDA183E4818D2ceaF58253CcAb3428",
    "orderId": "c0ab9ec2-8d33-41e6-bb37-5b88435d3479",
    "signature": "0xcd728264cad44fdee67b56e531937743400ed477de4c6d2d364e9c44a618b40e068d9b6364a7c7e86e36fc799aafc99b0c6b365cedcc1b4b4d4fc71a29f0e2691b"
}'
```

**Parameters:**

| Name      | Type   | Description                  |
| --------- | ------ | ---------------------------- |
| user      | string | Address for the listing user |
| orderId   | string | Listing order ID             |
| signature | string | Signature of the order ID    |

**Example response:**

```json
{
  "message": "success",
  "statusCode": 200
}
```

---

## Get NFT transaction history

Endpoint : `GET /marketplace/transaction-history/:contractAddress/:tokenId`

**Request**

```sh
curl --location '{{apiUrl}}marketplace/transaction-history/0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344/18'
```

**Parameters:**

| Name            | Type   | Description                 |
| --------------- | ------ | --------------------------- |
| contractAddress | string | Address of the NFT contract |
| tokenId         | string | Token ID of the NFT         |

**Example response:**

```json
{
  "message": {
    "MintData": {
      "NftContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
      "NftTokenId": "18",
      "TokenUri": "https://ipfs.io/ipfs/QmZcH4YvBVVRJtdn4RdbaqgspFU8gH6P9vomDpBVpAL3u4/18",
      "MintedBy": "0x46714661eecb6f07065dcb4bf3d9b772dcefa63a",
      "MintedAt": "2023-05-09T17:05:20.018447+05:30"
    },
    "Transactions": [
      {
        "OrderId": "0c27ecb1-0551-461c-87ae-e38506bec225",
        "FromUser": "0xccff350ef46b85228d6650a802107e58bf6a32ab",
        "ToUser": "0x1b34b2f706cda183e4818d2ceaf58253ccab3428",
        "Currency": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
        "ListAmount": "2",
        "BuyAmount": "2",
        "NftContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
        "NftTokenId": "18",
        "CreatedAt": "2023-05-16T11:30:44.449332+05:30"
      },
      {
        "OrderId": "95f0df4a-d5b6-4ee1-aaf4-f4ad3ba2cf4c",
        "FromUser": "0x1b34b2f706cda183e4818d2ceaf58253ccab3428",
        "ToUser": "0xccff350ef46b85228d6650a802107e58bf6a32ab",
        "Currency": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
        "ListAmount": "2",
        "BuyAmount": "2",
        "NftContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
        "NftTokenId": "18",
        "CreatedAt": "2023-05-15T19:40:10.428619+05:30"
      }
    ]
  },
  "statusCode": 200
}
```

---
