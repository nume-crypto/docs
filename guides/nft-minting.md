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
    "name": "NumeNFT",
    "owner": "0x46714661eecb6f07065dcb4bf3d9b772dcefa63a",
    "contractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
    "mintUsers": ["0xDc42d1dd82217013B79EBA43673912C4a3fC7bEA", "0x447bF33F7c7C925eb7674bCF590AeD4Aa57e656b","0x7771E6fE5245A04a94329A71b5c37aAcC22cCf53"],
    "lastTokenId": 0,
    "baseUri": "https://ipfs.io/ipfs/QmVLbfDpBj9XxXCCgWwhshpAQE9X23skZ8SfpUPn29HhnQ"
    "signature": "0xde67fa0f8964a6f35408ee724ea57ab55e262030830b6ce4d1bcd1ef397b5c3969cfccd457a41318fefd1087ad51aa85cb270df9981ed49f4df9bb5a6e3499e01b"
}'
```

**Parameters**

| Name            | Type   | Description                                  |
| --------------- | ------ | -------------------------------------------- |
| name            | string | Name of the NFT collection                   |
| owner           | string | Creator/Owner address of the NFT collection  |
| contractAddress | string | Contract address of the NFT collection on zkEVM |
| mintUsers       | array  | Users that can mint the NFTs on Nume         |
| lastTokenId     | number | Last tokenId of the NFT minted on zkEVM         |
| baseUri         | string | Base URI of the NFT collection               |
| signature       | string | User signs hash of NFT contract address, owner address, last token id   |

**Example response:**

```json
{
    "message": "success",
    "statusCode": 200
}
```

------------------------------------------------------------------------------------------------------------------

# Mint the NFT

Allows minting of NFT to an address on Nume.

**Endpoint** `POST /mint-nft`

**Request**

```sh
curl --location 'https://api.numecrypto.com/v2/mint-nft' \
--header 'Content-Type: application/json' \
--data '{
    "contractAddress": "0x6D9E72D1336e3592F5E4844B9e18E484fC4cf344",
    "MintUser": "0x46714661eecb6f07065dcb4bf3d9b772dcefa63a",
    "signature": "0x6d8d2cf296b39d8415f4c775f915d4b9e4561ed72fcc1da3c1380582193d423969a5000c2806dd2e3362d110165dd56d727a1bdb668c8ebacedfc1c6fd472c5d1c"
}'
```

**Parameters**

| Name            | Type   | Description                  |
| --------------- | ------ | ---------------------------- |
| contractAddress | string | Contract address of the NFT  |
| MintUser        | string | Recipient address of the NFT |
| signature       | string | User signs hash of NFT contract address, mint user address|

**Example response:**

```json
{
    "message": {
        "ContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
        "MintUser": "0x46714661eecb6f07065dcb4bf3d9b772dcefa63a",
        "NftTokenId": "19"
    },
    "statusCode": 200
}
```

------------------------------------------------------------------------------------------------------------------
