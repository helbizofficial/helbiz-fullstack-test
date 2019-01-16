### [Helbiz](https://helbiz.com) - Full-stack technical test
This test is part of our hiring process at Helbiz for full-stack Software Engineering positions. There are three stages to this test, but you shouldn’t spend more than 4-6 hours completing it. And don't worry if you can't complete everything!

Overview
------
We would like to see how you architect a simple application that does three things:

1. pulls data from an API that related to cryptocurrency wallets
2. manages an _internal_ balance system to transfer tokens between wallets
3. reads from the [Ethereum](https://www.ethereum.org/) blockchain using [web3.js](https://github.com/ethereum/web3.js/), an open-source library

Your code will be interacting with our testing environment, so don’t worry about breaking anything! The goal is for you to show us your coding style, best practices you follow, and demonstrate an understanding of APIs and your framework of choice.

Instructions
------
### 1. Wallets API
You are to use the first API to retrieve a list of addresses and ids, and only render the wallet addresses. You should also be able to filter them with a radio button and utilizing the `filter` API param. When you click on one of the wallets, display the information you retrieve with the second API.

Make API requests to this URL, and make sure to set the authorization header!

**API base URL** : `http://hbz-listen-test.us-west-2.elasticbeanstalk.com`

**Bearer token** : `HBZ90468f48ff6136f1`

#### --- Endpoint 1: Get list of wallets

Get all the wallet records, or only those assigned to a user, or only those with a positive HBZ balance

**PATH** : `/api/wallets`

**Method** : `GET`

**Params** : `filter [all|claimed|deposited]`

**Responses** : `400 BAD REQUEST`, `200 OK`

Example `200` response:
```json
{
  "filter": "all",
  "count": 1,
  "wallets": [
    {
      "_id": "5c0f...",
      "public_key": "0x7233..."
    }
  ]
}
```

#### --- Endpoint 2: Get wallet info

Get the wallet record with the given `_id`

**PATH** : `/api/wallets/show`

**Method** : `GET`

**Params** : `_id`

**Responses** : `400 BAD REQUEST`, `404 NOT FOUND`, `200 OK`

Example `200` response:
```json
{
  "public_key": "0x7233...",
  "created_at": "2019-01-01T17:12:43.123Z",
  "updated_at": "2019-01-01T17:53:59.158Z",
  "balance_hbz": 1000,
  "last_deposit_at": "2019-01-01T17:53:59.158Z",
  "last_deposit_tx": "0x7233.."
}
```

### 2. Internal Transfers
Provide a simple form that simulates a transfer between two wallets. For input, you'll need the `from` wallet address, `to` wallet address, and `amount` of HBZ to transfer. Persist these transfers using [mongoDB](https://www.mongodb.com/) and apply the transactions every time you pull data from the wallets API (again, consider an optimization strategy here).

### 3. Get ETH Balance Using web3.js
Finally - our API is only returning the HBZ balance for wallets. We would also like you to use the **web3.js** library to retrieve each wallet's ETH balance and display alongside the HBZ balance. Read the [API documentation](https://web3js.readthedocs.io/en/1.0/web3-eth.html#getbalance) to learn how to achieve this. All you need for this API is the wallet address.

Hint: To initialize the library, you need to [set a provider](https://web3js.readthedocs.io/en/1.0/web3.html#setprovider):
1. use library [truffle-privatekey-provider](https://www.npmjs.com/package/truffle-privatekey-provider) as the provider
2. [Infura](https://infura.io/) for the Ethereum client URL
3. and set the private key (account has 1 ETH) to => `76F6EC7EACC0F19FCA5CCB1D689A60B229327BF0C038119EE2BDFA2293236AFD`

Bonus points: Initialize the library with a websocket provider and update the webpage with every deposit for both ETH and HBZ.

Get coding!
------

To start, fork this repository and submit a pull request with your finished app. We'll review and schedule a call so you can go over it with us. Be prepared to explain your code and why you made some of the decisions you made.
