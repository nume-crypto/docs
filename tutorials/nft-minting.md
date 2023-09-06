# NFT minting tutorial

In this tutorial we will create an NFT collection and mint NFTs on Nume. Basic knowledge of javascript is sufficient to complete this tutorial. You need nodejs installed on your machine and use any of your favourite code editor.

While creating the metadata urls for the NFTs, we recommend you to follow this format `baseuri/tokenid`, so that every NFT that is being minted will have the unique metadata url to avoid duplicates and cunfusion between token ids on Nume and on L1.

> Example

Let us consider this as our base uri for the NFT collection `https://ipfs.io/ipfs/QmZcH4YvBVVRJtdn4RdbaqgspFU8gH6P9vomDpBVpAL3u4`

Then metadata url for the NFT with token id 1 should be `https://ipfs.io/ipfs/QmZcH4YvBVVRJtdn4RdbaqgspFU8gH6P9vomDpBVpAL3u4/1`

Currently token id of NFT is handled by Nume, so following this format will make NFT collection creation and NFT minting process smooth.

# Deploy a sample ERC721 (NFT) contract on zkEVM

If you are familiar to NFT contract development, feel free to create your own contract and deploy using any tool/framework.

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
const personalSignCreateNft = async (
  user,
  nftContractAddress,
  firstTokenId,
  lastTokenId,
  mintUsers,
  mintFees,
  mintFeesToken,
  royaltyPercent,
  baseUri,
  privateKey
) => {
  const provider = ethers.getDefaultProvider("mainnet");
  const wallet = new ethers.Wallet(privateKey, provider);
  try {
    const types = [];
    const values = [];
    mintUsers.forEach((mintUser) => {
      types.push("uint256");
      values.push(mintUser);
    });
    const mintUsersHash = ethers.utils.solidityKeccak256(types, values);
    const baseUriHash = ethers.utils.solidityKeccak256(["string"], [baseUri]);
    const hash = ethers.utils.solidityKeccak256(
      [
        "address",
        "address",
        "uint256",
        "uint256",
        "bytes32",
        "uint256",
        "address",
        "uint256",
        "bytes32",
      ],
      [
        nftContractAddress,
        user,
        firstTokenId,
        lastTokenId,
        mintUsersHash,
        mintFees,
        mintFeesToken,
        royaltyPercent,
        baseUriHash,
      ]
    );
    const signature = await wallet.signMessage(hash.slice(2));
    return signature;
  } catch (error) {
    console.error("Error:", error);
  }
};
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
const signature = await personalSignCreateNft(
  "0x447bF33F7c7C925eb7674bCF590AeD4Aa57e656b",
  "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344",
  "0",
  "100",
  ["0x447bF33F7c7C925eb7674bCF590AeD4Aa57e656b"],
  "1000000000000000000",
  "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
  "0",
  "https://ipfs.io/ipfs/QmVLbfDpBj9XxXCCgWwhshpAQE9X23skZ8SfpUPn29HhnQ",
  PRIVATE_KEY
);
const requestData = {
  name: "NumeNFT", // name of the NFT collection
  owner: "0x447bF33F7c7C925eb7674bCF590AeD4Aa57e656b", // owner address of the collection
  contractAddress: "0x6d9e72d1336e3592f5e4844b9e18e484fc4cf344", // contract address of the collection on zkEVM
  mintUsers: ["0x447bF33F7c7C925eb7674bCF590AeD4Aa57e656b"], // array of addresses that can mint NFTs from collection on Nume
  firstTokenId: "0", // first token id mint of the collection on Nume
  lastTokenId: "100", // last token id mint of the collection on Nume
  baseUri:
    "https://ipfs.io/ipfs/QmVLbfDpBj9XxXCCgWwhshpAQE9X23skZ8SfpUPn29HhnQ", // base uri of the collection (will be used for metadata of NFTs)
  mintFees: "1000000000000000000", // mint fee applied for every NFT mint in the collection (goes to the creator / collection owner)
  mintFeesToken: "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80", // address of the minting fee token
  royaltyFeesPercetage: "0", // percentage of royalty on secondary sales (goes to the creator / collection owner)
  signature,
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
const personalSignMintNft = async (
  user,
  nftContractAddress,
  mintFee,
  mintFeeCurrency,
  numeFee,
  nonce,
  privateKey
) => {
  const provider = ethers.getDefaultProvider("mainnet");
  const wallet = new ethers.Wallet(privateKey, provider);
  try {
    const hash = ethers.utils.solidityKeccak256(
      ["uint256", "address", "address", "uint256", "address", "uint256"],
      [nonce, nftContractAddress, user, mintFee, mintFeeCurrency, numeFee]
    );
    const signature = await wallet.signMessage(hash.slice(2));
    return signature;
  } catch (error) {
    console.error("Error:", error);
  }
};
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
const signature = await personalSignMintNft(
  "0x1daFCD50E221CFB70B5Be871f5E4556B9AD43Dcd",
  "0x6D9E72D1336e3592F5E4844B9e18E484fC4cf344",
  "1000000000000000000",
  "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
  "100000000000000000",
  2,
  0,
  PRIVATE_KEY
);
const data = {
  contractAddress: "0x6D9E72D1336e3592F5E4844B9e18E484fC4cf344", // contract address of the NFT collection
  MintUser: "0x1daFCD50E221CFB70B5Be871f5E4556B9AD43Dcd", // recipient address to which the NFT to be minted
  nonce: 2, // nonce of the user
  signature,
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
    "MintUser": "0x1dafcd50e221cfb70b5be871f5e4556b9ad43dcd",
    "NftTokenId": "1"
  },
  "statusCode": 200
}
```

- Run the javascript file

```sh
node ./index.js
```
