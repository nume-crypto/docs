# Nume indexer apis

## Fetch token balances

Endpoint : `POST /indexer/v1/nume/address/:address`

**Request**
```sh
curl --location 'https://api.protocol.numecrypto.com/v2/indexer/v1/nume/address/0x46714661eECB6F07065DCb4BF3D9b772dcefa63a/assets'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| address          | string      | retrieve balance tied to a particular address  |

**Example response:**

```json
[
    {
        "contract_name": "DAI",
        "contract_ticker_symbol": "DAI",
        "contract_decimals": 18,
        "contract_address": "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
        "coin": 31337,
        "type": "ERC20",
        "balance": "8900000000000000000",
        "quote": 8.898919324006927,
        "quote_rate": 0.9998785757311154,
        "logo_url": "https://api.protocol.numecrypto.com/v2/assets/images/dai.svg",
        "quote_rate_24h": "0",
        "quote_pct_change_24h": 0,
        "verified": true,
        "coin_gecko_id": ""
    },
    {
        "contract_name": "Ether",
        "contract_ticker_symbol": "ETH",
        "contract_decimals": 18,
        "contract_address": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
        "coin": 31337,
        "type": "ERC20",
        "balance": "3905263157894737",
        "quote": 6.816630930323962,
        "quote_rate": 1745.4984862015535,
        "logo_url": "https://api.protocol.numecrypto.com/v2/assets/images/eth.svg",
        "quote_rate_24h": "0",
        "quote_pct_change_24h": 0,
        "verified": true,
        "coin_gecko_id": ""
    }
]
```

-------------------------------------------------------------------------------------------------------

## Fetch token balances paginated

Endpoint : `POST /indexer/v2/nume/address/:address?pageSize=10&offset=0`

**Request**
```sh
curl --location 'https://api.protocol.numecrypto.com/v2/indexer/v2/nume/address/0x46714661eecb6f07065dcb4bf3d9b772dcefa63a/assets?pageSize=1&offset=0'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| address          | string      | retrieve balance tied to a particular address  |
| pageSize          | number      | number of records to return  |
| offset          | number      | offset of records to return  |

**Example response:**

```json
{
    "items_on_page": 2,
    "next_offset": 0,
    "assets": [
        {
            "contract_name": "DAI",
            "contract_ticker_symbol": "DAI",
            "contract_decimals": 18,
            "contract_address": "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
            "coin": 31337,
            "type": "ERC20",
            "balance": "8900000000000000000",
            "quote": 0,
            "quote_rate": 0,
            "logo_url": "https://api.protocol.numecrypto.com/v2/assets/images/dai.svg",
            "quote_rate_24h": "0",
            "quote_pct_change_24h": 0,
            "verified": true,
            "coin_gecko_id": ""
        },
        {
            "contract_name": "Ether",
            "contract_ticker_symbol": "ETH",
            "contract_decimals": 18,
            "contract_address": "0x0b6D9aB4c80889b65A61050470CBC5523d8Ce48D",
            "coin": 31337,
            "type": "ERC20",
            "balance": "3905263157894737",
            "quote": 0,
            "quote_rate": 0,
            "logo_url": "https://api.protocol.numecrypto.com/v2/assets/images/eth.svg",
            "quote_rate_24h": "0",
            "quote_pct_change_24h": 0,
            "verified": true,
            "coin_gecko_id": ""
        }
    ]
}
```

-------------------------------------------------------------------------------------------------------

## Fetch transaction history

Endpoint : `POST /indexer/v3/nume/address/:address?page=0&pageSize=5`

**Request**
```sh
curl --location 'https://api.protocol.numecrypto.com/v2/indexer/v3/nume/address/0xa9b39cb5ebf5deb0818561e8bc64092fbde34613/transactions?page=0&pageSize=5'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| address          | string      | retrieve balance tied to a particular address  |
| pageSize          | number      | number of records to return  |
| page          | number      | page to return  |


**Example response:**

```json
{
    "page": 1,
    "items_on_page": 3,
    "has_next": false,
    "transactions": [
        {
            "id": "0x1f31ac40e30c1b2d893185bd3df74a0617754d05ba754e81679dcc0ca11ed582",
            "from": "0x995227bd4dbfcd247fd7c97edba86c4ad46bfb05",
            "to": "0xa9b39cb5ebf5deb0818561e8bc64092fbde34613",
            "fee": "50000000000000000",
            "gas_price": "2000000000000",
            "gas_limit": "25000",
            "gas_used": "25000",
            "contract_address": "0xE9573B8A0AF951431bcBD194E8cc3AeE654Cd723",
            "date": 1686746529,
            "status": "completed",
            "type": "send",
            "block": 1,
            "value": "270000",
            "nonce": 2,
            "native_token_decimals": 18,
            "description": "Sent 0.270000 USDC",
            "sent": [
                {
                    "name": "USDC",
                    "symbol": "USDC",
                    "token_id": "0xE9573B8A0AF951431bcBD194E8cc3AeE654Cd723",
                    "decimals": 6,
                    "value": "270000",
                    "logo_url": "https://api.protocol.numecrypto.com/v2/assets/images/usdc.svg",
                    "from": "0x995227bd4dbfcd247fd7c97edba86c4ad46bfb05",
                    "to": "0xa9b39cb5ebf5deb0818561e8bc64092fbde34613"
                }
            ],
            "received": [],
            "input_data": "0x"
        },
        {
            "id": "0x83920b5aa6675869cdf5bfa290a1fa2b2ea89a4002c4f7b30f469c99af0435d0",
            "from": "0xa9b39cb5ebf5deb0818561e8bc64092fbde34613",
            "to": "0xdc42d1dd82217013b79eba43673912c4a3fc7bea",
            "fee": "50000000000000000",
            "gas_price": "2000000000000",
            "gas_limit": "25000",
            "gas_used": "25000",
            "contract_address": "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
            "date": 1686746527,
            "status": "completed",
            "type": "receive",
            "block": 1,
            "value": "660000000000000000",
            "nonce": 1,
            "native_token_decimals": 18,
            "description": "Received 0.660000 DAI",
            "sent": [],
            "received": [
                {
                    "name": "DAI",
                    "symbol": "DAI",
                    "token_id": "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
                    "decimals": 18,
                    "value": "660000000000000000",
                    "logo_url": "https://api.protocol.numecrypto.com/v2/assets/images/dai.svg",
                    "from": "0xa9b39cb5ebf5deb0818561e8bc64092fbde34613",
                    "to": "0xdc42d1dd82217013b79eba43673912c4a3fc7bea"
                }
            ],
            "input_data": "0x"
        },
        {
            "id": "0x6cf2fa8ea176c6ee54471086e07bca7315822b6e8b6999363b0a6d940f040362",
            "from": "0x11c830b25a15e39006094377fdc409c11c002b48",
            "to": "0xa9b39cb5ebf5deb0818561e8bc64092fbde34613",
            "fee": "50000000000000000",
            "gas_price": "2000000000000",
            "gas_limit": "25000",
            "gas_used": "25000",
            "contract_address": "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
            "date": 1686746502,
            "status": "completed",
            "type": "send",
            "block": 1,
            "value": "280000000000000032",
            "nonce": 1,
            "native_token_decimals": 18,
            "description": "Sent 0.280000 DAI",
            "sent": [
                {
                    "name": "DAI",
                    "symbol": "DAI",
                    "token_id": "0xEe146Fac7b2fce5FdBE31C36d89cF92f6b006F80",
                    "decimals": 18,
                    "value": "280000000000000032",
                    "logo_url": "https://api.protocol.numecrypto.com/v2/assets/images/dai.svg",
                    "from": "0x11c830b25a15e39006094377fdc409c11c002b48",
                    "to": "0xa9b39cb5ebf5deb0818561e8bc64092fbde34613"
                }
            ],
            "received": [],
            "input_data": "0x"
        }
    ]
}
```

-------------------------------------------------------------------------------------------------------

## Fetch transaction details

Endpoint : `POST /indexer/v1/nume/transactions/:transactionHash`

**Request**
```sh
curl --location 'https://api.protocol.numecrypto.com/v2/indexer/v1/nume/transactions/0x1f31ac40e30c1b2d893185bd3df74a0617754d05ba754e81679dcc0ca11ed582'
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| transactionHash          | string      | retrieve data of that transaction hash  |

**Example response:**

```json
{
    "id": "0x1f31ac40e30c1b2d893185bd3df74a0617754d05ba754e81679dcc0ca11ed582",
    "from": "0x995227bd4dbfcd247fd7c97edba86c4ad46bfb05",
    "to": "0xa9b39cb5ebf5deb0818561e8bc64092fbde34613",
    "fee": "50000000000000000",
    "gas_price": "2000000000000",
    "gas_limit": "25000",
    "gas_used": "25000",
    "contract_address": "0xE9573B8A0AF951431bcBD194E8cc3AeE654Cd723",
    "date": 1686746529,
    "status": "completed",
    "type": "send",
    "block": 1,
    "value": "270000",
    "nonce": 2,
    "native_token_decimals": 18,
    "description": "SENT 0.270000 USDC",
    "sent": [
        {
            "name": "USDC",
            "symbol": "USDC",
            "token_id": "0xE9573B8A0AF951431bcBD194E8cc3AeE654Cd723",
            "decimals": 6,
            "value": "270000",
            "logo_url": "https://api.protocol.numecrypto.com/v2/assets/images/usdc.svg",
            "from": "0x995227bd4dbfcd247fd7c97edba86c4ad46bfb05",
            "to": "0xa9b39cb5ebf5deb0818561e8bc64092fbde34613"
        }
    ],
    "received": null,
    "input_data": "0x"
}
```

-------------------------------------------------------------------------------------------------------
