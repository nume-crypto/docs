# Nume subscription apis

## Fetch subscription status

Endpoint : `POST /has-subscription/:address`

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
