# NFT minting tutorial

In this tutorial we will create an NFT collection and mint NFTs on Nume. Basic knowledge of javascript is sufficient to complete this tutorial. You need nodejs installed on your machine and use any of your favourite code editor.

While creating the metadata urls for the NFTs, we recommend you to follow this format `baseuri/tokenid`, so that every NFT that is being minted will have the unique metadata url to avoid duplicates and cunfusion between token ids on Nume and on L1.

> Example

Let us consider this as our base uri for the NFT collection `https://ipfs.io/ipfs/QmZcH4YvBVVRJtdn4RdbaqgspFU8gH6P9vomDpBVpAL3u4`

Then metadata url for the NFT with token id 1 should be `https://ipfs.io/ipfs/QmZcH4YvBVVRJtdn4RdbaqgspFU8gH6P9vomDpBVpAL3u4/1`

Currently token id of NFT is handled by Nume, so following this format will make NFT collection creation and NFT minting process smooth.

- Create a new folder for this project

```sh
mkdir numeNFTCollection
cd numeNFTCollection
```

- Create a javascript file (index.js)

# NFT collection creation

Make an API request to create an NFT (Non-Fungible Token) collection using the Numecrypto API.

```js
const url = "http://api.numecrypto.com/v2/create-nft-collection";
const apiKey = "NUME-API-KEY";

function callAPI(url, apiKey, data) {
  return fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "NUME-API-KEY": apiKey,
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
  name: "", // name of the NFT collection
  owner: "", // owner address of the collection
  contractAddress: "", // contract address of the collection on L1
  mintUsers: [""], // array of addresses that can mint NFTs from collection on Nume
  lastTokenId: 0, // last minted token id on l1 (token id continuation will be done to avoid confusion)
  baseUri: "", // base uri of the collection (will be used for metadata of NFTs)
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
const url = "http://api.numecrypto.com/v2/mint-nft";
const apiKey = "NUME-API-KEY";

function callAPI(url, apiKey, data) {
  return fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "NUME-API-KEY": apiKey,
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
  contractAddress: "", // contract address of the NFT collection
  MintUser: "", // recipient address to which the NFT to be minted
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
    "ContractAddress": "",
    "MintUser": "",
    "NftTokenId": 0
  },
  "statusCode": 200
}
```

- Run the javascript file

```sh
node ./index.js
```
