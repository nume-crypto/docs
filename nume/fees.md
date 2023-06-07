
# Fees 
?> **The protocol does not have gas instead we monetize through extremely low cost, fixed, flat fee on certain functions.**

Fees are additional amounts that a user pays to the network for the use of the network. Fees are paid in the native token of the network which is DAI. List of fees are as follows:


| Operation       | Definition   | Cost (per transaction)    |
|---------------|-------------|-------------|
| Token sends (DAI)     | DAI sends                  |Free     | 
| Token sends (other tokens)     | Sending other supported token on the Nume network: USDC, USDT, WBTC, MATIC, ETH      | 0.05 DAI      |
| NFT sends         | One-directional NFT send - nothing is received in return                   | 0.05 DAI      |
| NFT mints          | Minting an NFT                   | 0.10 DAI      |
| NFT trades            | NFT is sent, payment (ERC-20) is received                  | 0.30 DAI    |
|Creator fee on trades    | NFT collection creators can choose to set either a fixed or a % royalty fee to be collected each time an NFT they created is traded.  *Royalties cannot be collected on NFT sends.                    | % (set by creator) - Not capped by the protocol |
|Creator fee on mints         | NFT collection creators can choose to set either a fixed to be collected upon minting of the NFT.               | fixed fee (set by creator) - Not capped by the protocol |