# NFT minting

> **ON THIS PAGE, WE COVER:**
>
> - How to deploy a NFT collection on Nume?
> - How to mint NFTs on Nume?
> - How can you view, buy and sell NFTs on Nume?
> - How to withdraw the NFT to layer 1?

# Creating NFT collection

Allows creation of NFT collection on Nume. Existing NFT collection on L1 can deploy the same on Nume, by pausing the minting on L1 and continuing the token id from L1 to L2. If it is the new collection on L2 then token id can start from zero.

**Endpoint** `POST /create-nft-collection`

**Request**

```sh
curl --location 'https://api.numecrypto.com/v2/create-nft-collection' \
--header 'Content-Type: application/json' \
--header 'NUME-API-KEY: NUME-API-KEY' \
--data '{
    "name": "",
    "owner": "",
    "contractAddress": "",
    "mintUsers": [],
    "lastTokenId": 0,
    "baseUri": ""
}'
```

**Parameters**

| Name            | Type   | Description                                  |
| --------------- | ------ | -------------------------------------------- |
| name            | string | Name of the NFT collection                   |
| owner           | string | Creator/Owner address of the NFT collection  |
| contractAddress | string | Contract address of the NFT collection on L1 |
| mintUsers       | array  | Users that can mint the NFTs on Nume         |
| lastTokenId     | number | Last tokenId of the NFT minted on L1         |
| baseUri         | string | Base URI of the NFT collection               |

---

# Mint the NFT

Allows minting of NFT to an address on Nume.

**Endpoint** `POST /mint-nft`

**Request**

```sh
curl --location 'https://api.numecrypto.com/v2/mint-nft' \
--header 'Content-Type: application/json' \
--header 'NUME-API-KEY: NUME-API-KEY' \
--data '{
    "contractAddress": "",
    "MintUser": ""
}'
```

**Parameters**

| Name            | Type   | Description                  |
| --------------- | ------ | ---------------------------- |
| contractAddress | string | Contract address of the NFT  |
| MintUser        | string | Recipient address of the NFT |

---

# View the NFT

Get data of a particular NFT

---

# Buy NFT

Buy NFTs on Nume marketplace

---

# Sell NFT

Sell NFTs on Nume marketplace

---

# Withdrawal to L1

Withdraw NFT from Nume to L1. Currently having L1 minting is compulsary for any NFT collection on Nume and it has to implement the **mintNFTFromNume** function to facilitate the withdrawal of NFTs from Nume to L1.

```sol
function mintNFTFromNume(address recipient, uint256 tokenId)
```

**Arguments**

| Name      | TYpe    | Description                             |
| --------- | ------- | --------------------------------------- |
| recipient | address | Recipient address of the NFT collection |
| tokenId   | uint256 | Token ID of the NFT                     |

It is highly recommended to seperate the other minting functions from the above one. And restrict the above function to be only called by numeProtocolAddress

```sol
---
address private numeProtocolAddress;
function mintNFTFromNume(address recipient, uint256 tokenId) external {
        require(
            msg.sender == numeProtocolAddress,
            "NumeNFTFactory: Only NUME Protocol can call this function"
        );
        _safeMint(recipient, tokenId);

        emit MintNFTFromNume(recipient, tokenId);
}
---
```

To facilitate change of numeProtocolAddress, implement the below function which can be called by the owner/operator of the L1 collection contract.

```sol
---
function changeNumenProtocolAddress(address _numeProtocolAddress) external {
        require(msg.sender == operator, "NumeNFTFactory: Only operator can call this function");
        numeProtocolAddress = _numeProtocolAddress;
}
---
```
