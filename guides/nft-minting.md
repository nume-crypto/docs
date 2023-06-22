# NFT minting

> **ON THIS PAGE, WE COVER:**
>
> - How to deploy a NFT collection on Nume?
> - How to mint NFTs on Nume?
> - How can you view, buy and sell NFTs on Nume?
> - How to withdraw the NFT to layer 1?

# Creating NFT collection

**Endpoint** `POST /create-nft-collection`

**Request**

```sh
curl --location 'https://api.numecrypto.com/v2/create-nft-collection' \
--header 'Content-Type: application/json' \
--data '{
    "name": "NFT Collection",
    "owner": "0x1daFCD50E221CFB70B5Be871f5E4556B9AD43Dcd",
    "contractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
    "mintUsers": ["0x1daFCD50E221CFB70B5Be871f5E4556B9AD43Dcd"],
    "lastTokenId": "100",
    "firstTokenId": "0",
    "baseUri": "https://ipfs.io/ipfs/QmVLbfDpBj9XxXCCgWwhshpAQE9X23skZ8SfpUPn29HhnQ",
    "mintFees": "1000000000000000000",
    "mintFeesToken": "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
    royaltyFeesPercetage: "0",
    "signature": "0xb487981ee17668ed12ad330398183bb9b98903f351e4344a695bba693c0b880e6b10ec2cb5edddd9029918c530a60540f24d0ba0c940a09d85e4beab76d4e6591c"
}'
```

**Parameters**

| Name                 | Type   | Description                                                               |
| -------------------- | ------ | ------------------------------------------------------------------------- |
| name                 | string | Name of the NFT collection                                                |
| owner                | string | Creator/Owner address of the NFT collection                               |
| contractAddress      | string | Contract address of the NFT collection on zkEVM                           |
| mintUsers            | array  | Users that can mint the NFTs on Nume                                      |
| lastTokenId          | string | Last tokenId of the NFT mint on Nume                                      |
| firstTokenId         | string | First tokenId of the NFT mint on Nume                                     |
| baseUri              | string | Base URI of the NFT collection                                            |
| mintFees             | string | Minting fee for the NFT, can be collected in any supported token on Nume  |
| mintFeesToken        | string | Address of the minting fee token                                          |
| royaltyFeesPercetage | string | Percentage of royalty on secondary sales                                  |
| signature            | string | User signs hash of body params (check NFT minting tutorial for more info) |

**Example response:**

```json
{
  "message": "success",
  "statusCode": 200
}
```

---

# Mint the NFT

Allows minting of NFT to an address on Nume.

**Endpoint** `POST /mint-nft`

**Request**

```sh
curl --location 'https://api.numecrypto.com/v2/mint-nft' \
--header 'Content-Type: application/json' \
--data '{
    "contractAddress": "0x6D9E72D1336e3592F5E4844B9e18E484fC4cf344",
    "MintUser": "0x1daFCD50E221CFB70B5Be871f5E4556B9AD43Dcd",
    "nonce": 2,
    "signature": "0xb68726e0a316e1248b54a448cf7077407c4c6e9c525e75dd73530d5ca3954189045e0ae1f6a797f052cbc439711f31011bfe81750ff14040c762431737dda4e31c"
}'
```

**Parameters**

| Name            | Type   | Description                                                |
| --------------- | ------ | ---------------------------------------------------------- |
| contractAddress | string | Contract address of the NFT                                |
| MintUser        | string | Recipient address of the NFT                               |
| nonce           | number | Nonce of the user                                          |
| signature       | string | User signs hash of NFT contract address, mint user address |

**Example response:**

```json
{
  "message": {
    "ContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
    "MintUser": "0x1dafcd50e221cfb70b5be871f5e4556b9ad43dcd",
    "NftTokenId": "1"
  },
  "statusCode": 200
}
```

---
