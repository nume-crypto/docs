# Nume subscription apis

## Fetch subscription status

Endpoint : `GET /has-subscription/:address`

**Request**

```sh
curl --location '{{apiUrl}}/has-subscription/0xef6Fce8a1c8F6a94D1c197141E737b60C9a77aB2'
```

**Parameters:**

| Name    | Type   | Description                                          |
| ------- | ------ | ---------------------------------------------------- |
| address | string | retrieve subscription status of a particular address |

**Example response:**

```json
{
  "message": {
    "HasSubscription": true,
    "SubscribedAt": "2023-09-25T07:32:25.518941Z",
    "HasSubscribedThisSettlement": false,
    "SubscriptionEndBlockNumber": "3971",
    "HasUnsubscribed": true,
    "PreviousSubscriptions": []
  },
  "statusCode": 200
}
```

---

## Take subscription

Endpoint : `POST /subscribe`

**Request**

```sh
curl --location '{{apiUrl}}subscribe' \
--header 'Content-Type: application/json' \
--data '{
  "address": ,
  "signature": ,
  "type": "subscribe",
  "nonce": userKeysData.json.message.Nonce + 1,
}'
```

**Parameters:**

| Name      | Type   | Description                             |
| --------- | ------ | --------------------------------------- |
| address   | string | address of the user                     |
| signature | string | signature signed on the message by user |
| type      | string | subscribe/unsubscribe                   |
| nonce     | number | nonce of the user                       |

**Refer here to fetch [nonce](./guides/user.md?id=fetch-user-data) of the user and [current settlement number](./guides/user.md?id=fetch-block-number).**

**Signature construction:**

```js
let message = ethers.utils
  .solidityKeccak256(
    ["address", "uint256", "uint256", "uint256"],
    [
      address, // address of the user
      1, // 1 for subscribe
      userKeysData.json.message.Nonce + 1, // nonce of the user
      bn.json.message.SettlementNumber, // current settlement number at which subscription is taken
    ]
  )
  .slice(2);
let signature = await signMessage.signMessageAsync({
  message,
});
```

**Example response:**

```json
{
  "message": "success",
  "statusCode": 200
}
```

---

## Cancel subscription

Endpoint : `POST /subscribe`

**Request**

```sh
curl --location '{{apiUrl}}subscribe' \
--header 'Content-Type: application/json' \
--data '{
  "address": ,
  "signature": ,
  "type": "unsubscribe",
  "nonce": userKeysData.json.message.Nonce + 1,
}'
```

**Parameters:**

| Name      | Type   | Description                             |
| --------- | ------ | --------------------------------------- |
| address   | string | address of the user                     |
| signature | string | signature signed on the message by user |
| type      | string | subscribe/unsubscribe                   |
| nonce     | number | nonce of the user                       |

**Refer here to fetch [nonce](./guides/user.md?id=fetch-user-data) of the user and [current settlement number](./guides/user.md?id=fetch-block-number).**

**Signature construction:**

```js
let message = ethers.utils
  .solidityKeccak256(
    ["address", "uint256", "uint256", "uint256"],
    [
      address, // address of the user
      0, // 0 for unsubscribe
      userKeysData.json.message.Nonce + 1, // nonce of the user
      bn.json.message.SettlementNumber, // current settlement number at which subscription is cancelled
    ]
  )
  .slice(2);
let signature = await signMessage.signMessageAsync({
  message,
});
```

**Example response:**

```json
{
  "message": "success",
  "statusCode": 200
}
```

---
