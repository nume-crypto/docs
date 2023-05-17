# NFT minting tutorial

In this tutorial we will create an NFT collection and mint NFTs on Nume. Basic knowledge of javascript is sufficient to complete this tutorial. You need nodejs installed on your machine and use any of your favourite code editor.

While creating the metadata urls for the NFTs, we recommend you to follow this format `baseuri/tokenid`, so that every NFT that is being minted will have the unique metadata url to avoid duplicates and cunfusion between token ids on Nume and on L1.

> Example

Let us consider this as our base uri for the NFT collection `https://ipfs.io/ipfs/QmZcH4YvBVVRJtdn4RdbaqgspFU8gH6P9vomDpBVpAL3u4`

Then metadata url for the NFT with token id 1 should be `https://ipfs.io/ipfs/QmZcH4YvBVVRJtdn4RdbaqgspFU8gH6P9vomDpBVpAL3u4/1`

Currently token id of NFT is handled by Nume, so following this format will make NFT collection creation and NFT minting process smooth.

# Deploy a sample ERC721 (NFT) contract on zkEVM

If you are familiar to NFT contract development, feel free to create your own contract and deploy using any tool/framework. 
<!-- To keep things simple for this tutorial we will create a NFT contract with minimal functions and use remix to deploy it on polygon mumbai. -->

<!-- - remix - it is a browser based smart contract developemnt environment
- polygon mumbai - we will deploy the contract on mumbai testnet, get some test matic from any faucet to deploy the collection and mint some NFTs

> Checkout the complete code [here](https://remix.ethereum.org/#code=Ly8gU1BEWC1MaWNlbnNlLUlkZW50aWZpZXI6IE1JVApwcmFnbWEgc29saWRpdHkgXjAuOC45OwoKaW1wb3J0ICJAb3BlbnplcHBlbGluL2NvbnRyYWN0c0A0LjguMy90b2tlbi9FUkM3MjEvRVJDNzIxLnNvbCI7CmltcG9ydCAiQG9wZW56ZXBwZWxpbi9jb250cmFjdHNANC44LjMvYWNjZXNzL093bmFibGUuc29sIjsKaW1wb3J0ICJAb3BlbnplcHBlbGluL2NvbnRyYWN0c0A0LjguMy91dGlscy9Db3VudGVycy5zb2wiOwoKY29udHJhY3QgTXlUb2tlbiBpcyBFUkM3MjEsIE93bmFibGUgewogICAgdXNpbmcgQ291bnRlcnMgZm9yIENvdW50ZXJzLkNvdW50ZXI7CgogICAgQ291bnRlcnMuQ291bnRlciBwcml2YXRlIF90b2tlbklkQ291bnRlcjsKCiAgICBjb25zdHJ1Y3RvcigpIEVSQzcyMSgiTXlUb2tlbiIsICJNVEsiKSB7fQoKICAgIGZ1bmN0aW9uIF9iYXNlVVJJKCkgaW50ZXJuYWwgcHVyZSBvdmVycmlkZSByZXR1cm5zIChzdHJpbmcgbWVtb3J5KSB7CiAgICAgICAgcmV0dXJuICJodHRwczovL2lwZnMuaW8vaXBmcy9RbVpjSDRZdkJWVlJKdGRuNFJkYmFxZ3NwRlU4Z0g2UDl2b21EcEJWcEFMM3U0IjsKICAgIH0KCiAgICBmdW5jdGlvbiBzYWZlTWludChhZGRyZXNzIHRvKSBwdWJsaWMgb25seU93bmVyIHsKICAgICAgICB1aW50MjU2IHRva2VuSWQgPSBfdG9rZW5JZENvdW50ZXIuY3VycmVudCgpOwogICAgICAgIF90b2tlbklkQ291bnRlci5pbmNyZW1lbnQoKTsKICAgICAgICBfc2FmZU1pbnQodG8sIHRva2VuSWQpOwogICAgfQp9Cg&lang=en&optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.18+commit.87f61d96.js) -->

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract NumeNFT is ERC721, Ownable {
    using Counters for Counters.Counter;

    Counters.Counter private _tokenIdCounter;

    constructor() ERC721("NumeNFT", "NN") {}

    function _baseURI() internal pure override returns (string memory) {
        return "https://ipfs.io/ipfs/QmVLbfDpBj9XxXCCgWwhshpAQE9X23skZ8SfpUPn29HhnQ";
    }

    function safeMint(address to) public {
        uint256 tokenId = _tokenIdCounter.current();
        _tokenIdCounter.increment();
        _safeMint(to, tokenId);
    }
}
```

<!-- Connect metmask on remix

![Remix Injected Metamask Connection](../images/nft/remix-injected.png)

Click on deploy to initiate contract creation transaction

![Remix Injected Metamask Deployment](../images/nft/remix-deploy.png)

Put the recipient address of the NFT and click on transact button of safeMint to mint the NFT

![Remix Injected Metamask Minting](../images/nft/remix-mint.png)

You can verify all these transactions using polygonscan. -->

- Create a new folder for this project

```sh
mkdir numeNFTCollection
cd numeNFTCollection
```

- Create a javascript file (index.js)

# NFT collection creation

Make an API request to create an NFT (Non-Fungible Token) collection using the Numecrypto API.

```js
const url = "https://api.numecrypto.com/v2/create-nft-collection";

function callAPI(url, apiKey, data) {
  return fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(data),
  })
    .then((response) => response.json())
    .then((data) => {
      console.log("API response:", data);
      return data;
    })
    .catch((error) => console.error("API error:", error));
}

const requestData = {
  name: "NumeNFT", // name of the NFT collection
  owner: "0x447bF33F7c7C925eb7674bCF590AeD4Aa57e656b", // owner address of the collection
  contractAddress: "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344", // contract address of the collection on zkEVM
  mintUsers: [
    "0xDc42d1dd82217013B79EBA43673912C4a3fC7bEA",
    "0x46714661eecb6f07065dcb4bf3d9b772dcefa63a",
    "0x7771E6fE5245A04a94329A71b5c37aAcC22cCf53",
  ], // array of addresses that can mint NFTs from collection on Nume
  lastTokenId: 0, // last minted token id on zkEVM (token id continuation will be done to avoid confusion)
  baseUri:
    "https://ipfs.io/ipfs/QmVLbfDpBj9XxXCCgWwhshpAQE9X23skZ8SfpUPn29HhnQ", // base uri of the collection (will be used for metadata of NFTs)
};

callAPI(url, apiKey, requestData).then((responseData) => {
  // Do something with the response data here
});
```

**Response**

Status code 200 will be returned for successful creation of NFT collection.

```json
{
  "message": "success",
  "statusCode": 200
}
```

---

# NFT minting

Make an API request to mint an NFT (Non-Fungible Token) using the Numecrypto API.

```js
const url = "https://api.numecrypto.com/v2/mint-nft";

function callAPI(url, apiKey, data) {
  return fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(data),
  })
    .then((response) => response.json())
    .then((data) => {
      console.log("API response:", data);
      return data;
    })
    .catch((error) => console.error("API error:", error));
}

const data = {
  contractAddress: "0x6D9E72D1336e3592F5E4844B9e18E484fC4cf344", // contract address of the NFT collection
  MintUser: "0x46714661eecb6f07065dcb4bf3d9b772dcefa63a", // recipient address to which the NFT to be minted
};

callAPI(url, apiKey, data)
  .then((response) => {
    console.log(response);
    // Do something with the response here
  })
  .catch((error) => console.error(error));
```

**Response**

Status code 200 will be returned for successful minting of NFT and a message object containing contract address, recipient address and token id of the NFT minted. Token id will be auto incremented continuing the last token id from its corresponding L1. And every NFT will have the metadata url in `baseuri/tokenid` format.

```json
{
  "message": {
    "ContractAddress": "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
    "MintUser": "0x46714661eecb6f07065dcb4bf3d9b772dcefa63a",
    "NftTokenId": 19
  },
  "statusCode": 200
}
```

- Run the javascript file

```sh
node ./index.js
```
