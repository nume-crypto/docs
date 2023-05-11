# Deep dive into nft collections and minting

> **ON THIS PAGE, WE COVER:**
>
> - What is creating collection and minting?
> - How are smart contracts and tokens related?
> - What is minting on Nume?

### Terminology

- **NFT Collection** - smart contract to facilitate minting, transfers etc
- **Minting** - creating a new NFT in the collection
- **Transfer** - send NFTs from one address to another
- **Withdrawal** - withdraw the NFT from Nume to L1

# Creating NFT collection

A collection is a smart contract that allows minting of NFTs. Let's create a sample NFT collection using openzeppelin libraries.

```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract contractName is ERC721, Ownable {
    using Counters for Counters.Counter;

    Counters.Counter private _tokenIdCounter;

    constructor() ERC721("Toek Name", "Toekn Symbol") {}

}
```

# Minting

Minting on Nume is same as minting on any L1, user submits a request to mint a token to an address with the collection address and it will be processed accordingly. Currently token id is handled by Nume to avoid any confusions, because there is a chance of same token being minted on L1 and also on Nume, this is duplication of NFTs and creates confusion among NFT holders. This way withdrawal to L1 can also be facilitated as NFTs with same token ids doesnt exist on both networks.

```sol
---
function safeMint(address to) public {
        uint256 tokenId = _tokenIdCounter.current();
        _tokenIdCounter.increment();
        _safeMint(to, tokenId);
}
---
```

# Transfer of NFTs

Transfer the NFT from one address to another

```sol
---
function transferFrom(address from, address to, uint256 tokenId) public virtual override {

        require(_isApprovedOrOwner(_msgSender(), tokenId), "ERC721: caller is not token owner or approved");

        _transfer(from, to, tokenId);
}
---
```

# Withdrawal of NFT to L1

Ownership of NFT will be verified on Nume and withdrawal request will be processed. The exisitng NFT on Nume will be burnt/destroyed and the same token will be minted for the owner address on L1. Having a L1 minting contract is compulsary as of now to facilitate the minting of NFT, and contract has to implement **mintNFTFromNume** function to allow minting of token on L1 by Nume.
