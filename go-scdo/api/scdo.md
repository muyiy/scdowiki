|Command                                                                     |   Full   |  Light   |  public  | private |
| --------------------------------------------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetInfo](#getinfo)                                                         | &#x2713; |          | &#x2713; |         |
| [GetBalance](#getbalance)                                                   | &#x2713; | &#x2713; | &#x2713; |         |
| [AddTx](#addtx)                                                             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetAccountNonce](#getaccountnonce)                                         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockHeight](#getblockheight)                                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlock](#getblock)                                                       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockByHash](#getblockbyhash)                                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockByHeight](#getblockbyheight)                                       | &#x2713; | &#x2713; | &#x2713; |         |
| [Call](#call)                                                               | &#x2713; |          | &#x2713; |         |
| [GetLogs](#getlogs)                                                         | &#x2713; |          | &#x2713; |         |
| [GetCode](#getcode)                                                         | &#x2713; |          | &#x2713; |         |
| [GeneratePayload](#generatepayload)                                         | &#x2713; |          | &#x2713; |         |
| [EstimateGas](#estimategas)                                                 | &#x2713; |          | &#x2713; |         |
| [GetBlockTransactionCount](#getblocktransactioncount)                       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionsFrom](#gettransactionsfrom)                                 | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionsTo](#gettransactionsto)                                     | &#x2713; | &#x2713; | &#x2713; |         |
| [GetAccountTransactions](#getaccounttransactions)                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionsByHeight](#getblocktransactionsbyheight)               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionsByHash](#getblocktransactionsbyhash)                   | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactions](#getblocktransactions)                               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionCountByHeight](#getblocktransactioncountbyheight)       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionCountByHash](#getblocktransactioncountbyhash)           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockIndex](#gettransactionbyblockindex)                   | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockHeightAndIndex](#gettransactionbyblockheightandindex) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockHashAndIndex](#gettransactionbyblockhashandindex)     | &#x2713; | &#x2713; | &#x2713; |         |
| [GetReceiptByTxHash](#getreceiptbytxhash)                                   | &#x2713; | &#x2713; | &#x2713; |         |



### scdo

RPC collection provided for public for blockchain node and transaction manipulation.

***

#### GetInfo

This method returns the node information.

| Type | Template                                                        |
| ---- | --------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getInfo","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `Coinbase`:`string` - node address
- `CurrentBlockHeight`:`uint64` - current block height
- `HeaderHash`:`string` - block hash
- `MinerStatus`:`string` - miner status
- `Shard`:`int` - shard number
- `Version`:`string` - version number of the node
- `BlockAge`:`big.Int` - the age of the latest block of the node
- `PeerCnt`:`string` - total peer count and the peer count of each shard  

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getInfo","params":[],"id":1}' localhost:8037
```
- Result

```js
{
   "jsonrpc": "2.0",
   "id": 1,
   "result": {
      "Coinbase": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
      "CurrentBlockHeight": 1759971,
      "HeaderHash": "0x64ac24b6463d2cf14b9fd8b1c38ea6347977b38f105f76e34baf24fcc46f6aaf",
      "Shard": 1,
      "MinerStatus": "Stopped",
      "Version": "v1.2.7",
      "BlockAge": -5,
      "PeerCnt": "11 (2 3 3 3)"
   }
}
```
***

#### GetBalance

This method returns the account balance given the account address.

| Type | Template                                                                                |
| ---- | --------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBalance","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `Account`:`string` - account
- `hexHash`:`string` - hex form of a block hash, set to "" for the latest balance
- `height` :`uint64` - height of a block, set to -1 for the latest balance

##### Returns

- `Account`:`string` - account
- `Balance`:`big.Int` - account balance

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBalance","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21","",-1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "Account": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
        "Balance": 265499990000
    }
}
```
***

#### AddTx

This method submits a transaction to the node.

| Type | Template                                                                       |
| ---- | ------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_addTx","params":[types.Transaction],"id":1}` |

##### Parameters

- `tx`:`types.Transaction` - transaction struct (client command `sign` could be used to get transaction hash and signature)
  - `Hash`:`string` - transaction hash
  - `Data`:`json` - transaction data
    - `From`:`string` - transaction sender
    - `To`:`string` - transaction receiver
    - `Amount`:`uint64` - amount value, unit is fan
    - `Fee`:`uint64` - transaction fee
    - `Payload`:`string` - transaction payload
    - `AccountNonce`:`uint64` - transaction nonce
  - `Signature` : `crypto.Signature` - transaction signature struct
   ```
  type Signature struct {
	   Sig []byte // [R || S || V] format signature in 65 bytes.
  }
  ```

##### Returns

- `result`:`bool` - transaction send result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_addTx","params":[{"Hash": "0x3393e5566cb905d714599f2f888ecc6d223b83403887460fa5b2771e89a0436e","Data": {"From": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21","To":"0x2a87b6504cd00af95a83b9887112016a2a991cf1","Amount": 1,"AccountNonce":0,"Fee": 0,"GasPrice":10, "GasLimit":21000},"Signature":{"Sig":"fAvgVTXDyJZbfv07NYBK4aSolfY4ycBPQRwnQFpHRMc7ooOZw27U50o4TBoRelYX3QCRyvKpbxVlxhu7AnSB6QE="}}],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": true
}
```
***

#### GetAccountNonce

This method is used to obtain the account nonce.

| Type | Template                                                                                     |
| ---- | -------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getAccountNonce","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - account
- `hexHash`:`string` - hex form of a block hash, set to "" for the latest nonce
- `height` :`uint64` - height of a block, set to -1 for the latest nonce

##### Returns

- `result`:`uint64` - account nonce

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getAccountNonce","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21","",-1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 3
}
```
***

#### GetBlockHeight

This method is used to obtain the height of the blockchain.

| Type | Template                                                               |
| ---- | ---------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockHeight","params":[],"id":1}` |

##### Parameters

none

##### Returns

- `result`:`uint64` - block height

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockHeight","params":[],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 1928
}
```
***

#### GetBlock

This method is used to obtain the block content based on block height or block hash.

| Type | Template                                                                           |
| ---- | ---------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlock","params":[string,string,bool],"id":1}` |

##### Parameters

- `hash`:`string` - block hash
- `height`:`string` - block height
- `fulltx, f`:`bool` - whether to include detailed transaction information

##### Returns

- `debts`:`array` - debts in block
  - `Hash`:`string` - debts hash
  - `Data`:`json` - debts data
  - `TxHash`:`string` - txhash in debt
  - `Shard`:`int` - shard number of scdo node where debts on
  - `Account`:`array` - debt account
  - `Amount`:`int64` - debt amount
  - `Fee`:`int64` - debt fee
  - `Code`:`string` - debt code
- `hash`:`string` - block hash
- `header`:`json` - block header
  - `PreviousBlockHash`:`string` - previous block hash
  - `Creator`:`string` - creator address
  - `TxHash`:`string` - tx hash
  - `ReceiptHash`:`string` - Receipts hash
  - `stateHash`:`string` - state tree hash
  - `TxDebtHash`:`string` - debts hash
  - `DebtHash`:`string` - debts hash
  - `Difficulty`:`big.Int` - block difficulty
  - `Height`:`unit64` - block height
  - `CreateTimestamp`:`uint64` - create timestamp
  - `Witness`:`string` - block nonce
  - `Consensus`:`int` - consensus algorithm
  - `ExtraData`:`string` - extra data
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
  - `accountNonce`:`unit64` - account nonce
  - `amount`:`Int` - transaction amount
  - `from`:`string` - transaction provider
  - `gasLimit`:`Int` - transaction gas limit
  - `gasPrice`:`Int` - transaction gas price
  - `hash`:`string` - transaction hash
  - `payload`:`array` - transaction payload
  - `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
  - `Hash`:`string` - txDebts hash
  - `Data`:`json` - txDebts data
    - `TxHash`:`string` - transaction hash
    - `From`:`string` - transaction sender
    - `Nonce`:`unit64` - sender nonce
    - `Account`:`string` - transaction account
    - `Amount`:`int` - transaction amount
    - `Price`:`int` - transaction gas price
    - `Code`:`string` - transaction code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlock","params":["",19018,true],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "debts": [],
        "hash": "0x000002f75910694bf33a9a2f3e0cab454ac4b14ff9d32aee7b59efc20260f00c",
        "header": {
            "PreviousBlockHash": "0x000005f39610211ad1e888940a0e6affb538ea2397f73e08f1f894537997118c",
            "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
            "StateHash": "0xde119fb11c8c74b34a71ce376589a1711af5acef99aaf36827fbaafaeb9fe617",
            "TxHash": "0xa5dea280e6e880af7547ffea5c54526b0a3fae9dcd977a0a5a00e14852eb08ce",
            "ReceiptHash": "0xd6efdf2db85d6a5ab3fdc14925f67b9c97fb7ebdb733e5b2bb5776c694bc9073",
            "TxDebtHash": "0x8fde2b990967a9e51cb5218acc3318faea7a50429760cef37867b12c62f30b78",
            "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "Difficulty": 2258387,
            "Height": 19018,
            "CreateTimestamp": 1548821456,
            "Witness": "MTI4ODU5Njk2MTcyODI5NzQ3MzM=",
            "Consensus": 0,
            "ExtraData": ""
        },
        "totalDifficulty": 52970343102,
        "transactions": [
            {
                "accountNonce": 0,
                "amount": 1200000000,
                "from": "0x0000000000000000000000000000000000000000",
                "gasLimit": 0,
                "gasPrice": 0,
                "hash": "0x0071c67a94f3619d9c7acb6fd40750956df24beb5dfaa5372e87a83bc06e219c",
                "payload": "",
                "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
            },
            {
                "accountNonce": 100,
                "amount": 88,
                "from": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                "gasLimit": 63000,
                "gasPrice": 10,
                "hash": "0xf7288fbc1ab3bea992dd5f311644f220b1accf8011f59df4778ca526843d1f68",
                "payload": "",
                "to": "0x007d1b1ea335e8e4a74c0be781d828dc7db934b1"
            }
        ],
        "txDebts": [
            {
                "Hash": "0xa0089462915e0a1b99ce3d75f6b51cdd5caf9a52691f327c9a27d222e0e38d57",
                "Data": {
                    "TxHash": "0xf7288fbc1ab3bea992dd5f311644f220b1accf8011f59df4778ca526843d1f68",
                    "From": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                    "Nonce": 100,
                    "Account": "0x007d1b1ea335e8e4a74c0be781d828dc7db934b1",
                    "Amount": 88,
                    "Price": 10,
                    "Code": ""
                }
            }
        ]
    }
}
```
***

#### GetBlockByHash

This method is used to obtain the block content based on block hash.

| Type | Template                                                                          |
| ---- | --------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockByHash","params":[string,bool],"id":1}` |

##### Parameters

- `hash`:`string` - block hash
- `fulltx, f`:`bool` - whether to include detailed transaction information

##### Returns

- `debts`:`array` - debts in block
  - `Hash`:`string` - debts hash
  - `Data`:`json` - debts data
  - `TxHash`:`string` - txhash in debt
  - `Shard`:`int` - shard number of scdo node where debts on
  - `Account`:`array` - debt account
  - `Amount`:`int64` - debt amount
  - `Fee`:`int64` - debt fee
  - `Code`:`string` - debt code
- `hash`:`string` - block hash
- `header`:`json` - block header
  - `PreviousBlockHash`:`string` - previous block hash
  - `Creator`:`string` - creator address
  - `TxHash`:`string` - tx hash
  - `ReceiptHash`:`string` - Receipts hash
  - `stateHash`:`string` - state tree hash
  - `TxDebtHash`:`string` - debts hash
  - `DebtHash`:`string` - debts hash
  - `Difficulty`:`big.Int` - block difficulty
  - `Height`:`unit64` - block height
  - `CreateTimestamp`:`uint64` - create timestamp
  - `Witness`:`string` - block nonce
  - `Consensus`:`int` - consensus algorithm
  - `ExtraData`:`string` - extra data
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
  - `accountNonce`:`unit64` - account nonce
  - `amount`:`Int` - transaction amount
  - `from`:`string` - transaction provider
  - `gasLimit`:`Int` - transaction gas limit
  - `gasPrice`:`Int` - transaction gas price
  - `hash`:`string` - transaction hash
  - `payload`:`array` - transaction payload
  - `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
  - `Hash`:`string` - txDebts hash
  - `Data`:`json` - txDebts data
    - `TxHash`:`string` - transaction hash
    - `From`:`string` - transaction sender
    - `Nonce`:`unit64` - sender nonce
    - `Account`:`string` - transaction account
    - `Amount`:`int` - transaction amount
    - `Price`:`int` - transaction gas price
    - `Code`:`string` - transaction code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockByHash","params":["0x000002f75910694bf33a9a2f3e0cab454ac4b14ff9d32aee7b59efc20260f00c",true],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "debts": [],
        "hash": "0x000002f75910694bf33a9a2f3e0cab454ac4b14ff9d32aee7b59efc20260f00c",
        "header": {
            "PreviousBlockHash": "0x000005f39610211ad1e888940a0e6affb538ea2397f73e08f1f894537997118c",
            "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
            "StateHash": "0xde119fb11c8c74b34a71ce376589a1711af5acef99aaf36827fbaafaeb9fe617",
            "TxHash": "0xa5dea280e6e880af7547ffea5c54526b0a3fae9dcd977a0a5a00e14852eb08ce",
            "ReceiptHash": "0xd6efdf2db85d6a5ab3fdc14925f67b9c97fb7ebdb733e5b2bb5776c694bc9073",
            "TxDebtHash": "0x8fde2b990967a9e51cb5218acc3318faea7a50429760cef37867b12c62f30b78",
            "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "Difficulty": 2258387,
            "Height": 19018,
            "CreateTimestamp": 1548821456,
            "Witness": "MTI4ODU5Njk2MTcyODI5NzQ3MzM=",
            "Consensus": 0,
            "ExtraData": ""
        },
        "totalDifficulty": 52970343102,
        "transactions": [
            {
                "accountNonce": 0,
                "amount": 1200000000,
                "from": "0x0000000000000000000000000000000000000000",
                "gasLimit": 0,
                "gasPrice": 0,
                "hash": "0x0071c67a94f3619d9c7acb6fd40750956df24beb5dfaa5372e87a83bc06e219c",
                "payload": "",
                "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
            },
            {
                "accountNonce": 100,
                "amount": 88,
                "from": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                "gasLimit": 63000,
                "gasPrice": 10,
                "hash": "0xf7288fbc1ab3bea992dd5f311644f220b1accf8011f59df4778ca526843d1f68",
                "payload": "",
                "to": "0x007d1b1ea335e8e4a74c0be781d828dc7db934b1"
            }
        ],
        "txDebts": [
            {
                "Hash": "0xa0089462915e0a1b99ce3d75f6b51cdd5caf9a52691f327c9a27d222e0e38d57",
                "Data": {
                    "TxHash": "0xf7288fbc1ab3bea992dd5f311644f220b1accf8011f59df4778ca526843d1f68",
                    "From": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                    "Nonce": 100,
                    "Account": "0x007d1b1ea335e8e4a74c0be781d828dc7db934b1",
                    "Amount": 88,
                    "Price": 10,
                    "Code": ""
                }
            }
        ]
    }
}
```
***

#### GetBlockByHeight

This method is used to obtain the block content based on block height.

| Type | Template                                                                            |
| ---- | ----------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockByHeight","params":[string,bool],"id":1}` |

##### Parameters

- `height`:`string` - block height
- `fulltx, f`:`bool` - whether to include detailed transaction information

##### Returns

- `debts`:`array` - debts in block
  - `Hash`:`string` - debts hash
  - `Data`:`json` - debts data
  - `TxHash`:`string` - txhash in debt
  - `Shard`:`int` - shard number of scdo node where debts on
  - `Account`:`array` - debt account
  - `Amount`:`int64` - debt amount
  - `Fee`:`int64` - debt fee
  - `Code`:`string` - debt code
- `hash`:`string` - block hash
- `header`:`json` - block header
  - `PreviousBlockHash`:`string` - previous block hash
  - `Creator`:`string` - creator address
  - `TxHash`:`string` - tx hash
  - `ReceiptHash`:`string` - Receipts hash
  - `stateHash`:`string` - state tree hash
  - `TxDebtHash`:`string` - debts hash
  - `DebtHash`:`string` - debts hash
  - `Difficulty`:`big.Int` - block difficulty
  - `Height`:`unit64` - block height
  - `CreateTimestamp`:`uint64` - create timestamp
  - `Witness`:`string` - block nonce
  - `SecondWitness`:`string` - second block nonce (degenerated)
  - `Consensus`:`int` - consensus algorithm
  - `ExtraData`:`string` - extra data
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
  - `accountNonce`:`unit64` - account nonce
  - `amount`:`Int` - transaction amount
  - `from`:`string` - transaction provider
  - `gasLimit`:`Int` - transaction gas limit
  - `gasPrice`:`Int` - transaction gas price
  - `hash`:`string` - transaction hash
  - `payload`:`array` - transaction payload
  - `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
  - `Hash`:`string` - txDebts hash
  - `Data`:`json` - txDebts data
    - `TxHash`:`string` - transaction hash
    - `From`:`string` - transaction sender
    - `Nonce`:`unit64` - sender nonce
    - `Account`:`string` - transaction account
    - `Amount`:`int` - transaction amount
    - `Price`:`int` - transaction gas price
    - `Code`:`string` - transaction code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockByHeight","params":[19018,true],"id":1}' localhost:8037
```
- Result

```js
{
   "jsonrpc": "2.0",
   "id": 1,
   "result": {
      "debts": [],
      "hash": "0x430216878d75c4beeb5218158e9920a664e5e883a8311600dd4cb21c91b8d9a2",
      "header": {
         "PreviousBlockHash": "0x359e1148e8eb8bb2bc0e7878fff034cba775df8338a71d65e3c0b48668f11c45",
         "Creator": "0xd63a23ba710c16fb121f53a4e38163a23c053e31",
         "StateHash": "0xe0a7e462dda0df064521581ef482c43460a8ae4a313f42513b6f67f688e3f5fd",
         "TxHash": "0x1555ed359bcc999483174709a48218f0c1871756441025937fc45f85bf11dc99",
         "ReceiptHash": "0xc1da588af38fb099399b8b2f8d98183c2934d903a973a90f326a9ce1115e3c1e",
         "TxDebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
         "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
         "Difficulty": 5990106,
         "Height": 19018,
         "CreateTimestamp": 1554386780,
         "Witness": "NTkwOTMxOTAwNTgwMDIzMDA4NQ==",
         "SecondWitness": "NTkwOTMxOTAwNTgwMDQxODM3NQ==",
         "Consensus": 0,
         "ExtraData": ""
      },
      "totalDifficulty": 108806815827,
      "transactions": [
         {
            "accountNonce": 0,
            "amount": 600000000,
            "from": "0x0000000000000000000000000000000000000000",
            "gasLimit": 0,
            "gasPrice": 0,
            "hash": "0x48e3e648f8231bd3b48e356ead95412511e0576aa5be3614da4a57d7badb80e9",
            "payload": "",
            "signature": {
               "Sig": ""
            },
            "to": "0xd63a23ba710c16fb121f53a4e38163a23c053e31"
         }
      ],
      "txDebts": []
   }
}
```
***

#### Call

This method is used to execute a given transaction on a statedb of a given block height. It does not affect the statedb or blockchain and is useful for executing and retrieving values. However, the height currently does not support optional and will remove the from parameter in the next version or more.

| Type | Template                                                                 |
| ---- | ------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_call ","params":[CallRequest],"id":1}` |

##### Parameters

- `to`:`string` - to address
- `payload`:`string` - transaction payload info
- `Height`:`int64` - block height (default: -1)

##### Returns

- `contract`:`string` - contract address
- `failed`:`bool` - contract executes successfully or not
- `poststate`:`string` - state trie root hash after transaction execution
- `result`:`string` - transaction result
- `totalFee`:`int64` - transaction fee
- `txhash`:`string` - transaction hash
- `usedGas`:`int64` - transaction gas

##### Example
When using the example below, the contract must be deployed first. The solidity code file:

```
pragma solidity ^0.4.0;

contract SimpleStorage {
    uint storedData=23;

    function set(uint x) {
        storedData=x;
    }

    function get() constant returns(uint) {
        return storedData;
    }
}
```
As you can see, the example is testing the get function.
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_call","params":["0x9df8ed11ea024183bd584480e80952c9b04e0122","0x6d4ce63c",-1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "contract": "0x",
        "failed": false,
        "poststate": "0xb724c37fd2047d26c7e22da0f43d8c520aa15d9fc9358872583eb4a11b9c6787",
        "result": "0x0000000000000000000000000000000000000000000000000000000000000005",
        "totalFee": 101,
        "txhash": "0xefaa679d7b6bbbf2b56b198f45156a82a737a352cb1d42f2f5357ed3a4f91a16",
        "usedGas": 424
    }
}
```
***

#### GetLogs

This method gets the event logs by block height, the contract address, and the event name.

| Type | Template                                                                       |
| ---- | ------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getLogs ","params":[GetLogsRequest],"id":1}` |

##### Parameters

- `height`:`int64` - block height (default: -1)
- `contract`:`string` - contract address
- `abi`:`string` - contract abi
- `event`:`string` - event name

##### Returns

- `address`:`string` - contract address
- `topics`:`array` - topic array
- `data`:`string` - data
- `blocknumber`:`uint64` - block height
- `transactionNumber`:`uint` - the index of the transaction in the block

##### Example
When using the example below, the contract must be deployed first. The solidity code file:

```
pragma solidity ^0.4.0;

contract simple_storage_1 {
    uint storedData=23;

    event getLog(address addr, string message);
    event getLog1(string message);
    event getLog2(string message);

    function set(uint x) public{
        getLog1("set getLog1");
        getLog2("set getLog2");
        storedData=x;
    }

    function get() constant public returns(uint) {
        getLog(msg.sender, "get getLog");
        getLog1("get getLog1");
        set(16);
        return storedData;
    }
}
```
As you can see, this example is testing the get function. In this situation, the height is the block height of the block containing the get transaction.
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getLogs","params":[1760936,"0x4df9ac0d329c07da15f202090649258c109a0022","[{\"constant\":false,\"inputs\":[{\"name\":\"x\",\"type\":\"uint256\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"addr\",\"type\":\"address\"},{\"indexed\":false,\"name\":\"message\",\"type\":\"string\"}],\"name\":\"getLog\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"message\",\"type\":\"string\"}],\"name\":\"getLog1\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"message\",\"type\":\"string\"}],\"name\":\"getLog2\",\"type\":\"event\"},{\"constant\":true,\"inputs\":[],\"name\":\"get\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]","getLog2"],"id":1}' localhost:8037
```
- Result

```js
{"jsonrpc":"2.0","id":1,"result":[{"address":"0x4df9ac0d329c07da15f202090649258c109a0022","topics":["0xe84bb31d4e9adbff26e80edeecb6cf8f3a95d1ba519cf60a08a6e6f8d62d8100"],"data":"0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000b736574206765744c6f6732000000000000000000000000000000000000000000","blockNumber":1760936,"transactionIndex":1}]}
```
***

#### GetCode

This method gets the contract code by block height and contract address.

| Type | Template                                                                      |
| ---- | ----------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getCode ","params":[string, int64],"id":1}` |

##### Parameters

- `contract`:`string` - contract address
- `height`:`int64` - block height (default: -1)

##### Returns

- `payload`:`string` - contract code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getCode","params":["0xe2b99c9e86ebe7b087ede32b2cca3a4b3ee10032", 1077640],"id":1}' localhost:8037
```
- Result

```js
{"jsonrpc":"2.0","id":1,"result":"0x610646610030600b82828239805160001a6073146000811461002057610022565bfe5b5030600052607381538281f300730000000000000000000000000000000000000000301460806040526004361061008f576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680634c5e1cae1461009457806375a3e8e8146100e857806388d0443714610159578063a21ab71614610197578063ab517b4f146101cb578063c8fccc691461023a575b600080fd5b6100d260048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff16906020019092919050505061027c565b6040518082815260200191505060405180910390f35b61011060048036038101908080359060200190929190803590602001909291905050506102cb565b604051808373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020018281526020019250505060405180910390f35b610181600480360381019080803590602001909291908035906020019092919050505061035d565b6040518082815260200191505060405180910390f35b6101b5600480360381019080803590602001909291905050506103c6565b6040518082815260200191505060405180910390f35b8180156101d757600080fd5b5061022060048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506103f9565b604051808215151515815260200191505060405180910390f35b6102626004803603810190808035906020019092919080359060200190929190505050610580565b604051808215151515815260200191505060405180910390f35b60008260000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060010154905092915050565b60008083600101838154811015156102df57fe5b9060005260206000200160000160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1691508360000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000206001015490509250929050565b60008082905080806001019150505b8360010180549050811080156103aa5750836001018181548110151561038e57fe5b9060005260206000200160000160149054906101000a900460ff165b156103bc57808060010191505061036c565b8091505092915050565b60006103f2827fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff61035d565b9050919050565b6000808460000160008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600001549050828560000160008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060010181905550600081111561049e5760019150610578565b8460010180548091906001016104b49190610594565b9050600181018560000160008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000206000018190555083856001018281548110151561051457fe5b9060005260206000200160000160006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff1602179055508460020160008154809291906001019190505550600091505b509392505050565b600082600101805490508210905092915050565b8154818355818111156105bb578183600052602060002091820191016105ba91906105c0565b5b505050565b61061791905b8082111561061357600080820160006101000a81549073ffffffffffffffffffffffffffffffffffffffff02191690556000820160146101000a81549060ff0219169055506001016105c6565b5090565b905600a165627a7a72305820b794fd1c17a9ff0d50981b40ff2dd307a38ab6776bc963e8a4bff7df0b11f5170029"}
```
***

#### GeneratePayload

This method generates the contract method payload.

| Type | Template                                                                                        |
| ---- | ----------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_generatePayload","params":[string, string, []string],"id":1}` |

##### Parameters

- `abiJSON`:`string` - contract json string
- `methodName`:`string` - contract method name
- `args`:`string` - args of contract method

##### Returns

- `result`:`string` payload of contract method with args

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_generatePayload","params":["[{\"constant\":false,\"inputs\":[{\"name\":\"x\",\"type\":\"uint256\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"get\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"inputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]", "set", ["1"]],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x60fe47b10000000000000000000000000000000000000000000000000000000000000001"
}
```
***

#### EstimateGas

This method estimates the gas of a transaction.

| Type | Template                                                                             |
| ---- | ------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_estimateGas","params":[types.Transaction],"id":1}` |

##### Parameters

- `Hash`:`string` - transaction hash
- `Data`:`json` - transaction data
  - `From`:`string` - transaction sender
  - `To`:`string` - transaction receiver
  - `Amount`:`uint64` - amount value, unit is fan
  - `GasPrice`:`uint64` - transaction gas price in Fan
  - `GasLimit`:`uint64` - maximum gas for transaction
  - `Payload`:`string` - transaction payload
  - `AccountNonce`:`uint64` - transaction nonce

##### Returns

- `result`:uint64 - gas amount

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_estimateGas","params":[{"Hash":"0xa56fc9d8fb292c989c61be57d3a2e77902d68331d19cfb689e491574c679b7a0","Data":{"Type":0,"From":"0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1","To":"0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1","Amount":10,"AccountNonce":64,"GasPrice":1,"GasLimit":21000,"Timestamp":0,"Payload":""},"Signature":{"Sig":"3a/HhtAao9QiLmGkjgcv2tRSsvMxx1myWJoCVYpaJ64T49rYmYWWpE0JCAjYVqPkK8t4V88C+0VTLKkBfd68+wA="}}],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 21000
}
```
***

#### GetBlockTransactionCount

This method is used to obtain the number of transactions in the block based on block height or hash.

| Type | Template                                                                                     |
| ---- | -------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockTransactionCount","params":[string,int64],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex
- `height`:`int64` - block height (default: -1)

##### Returns

- `result`:`int` - transactions count

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockTransactionCount","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922",-1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetBlockTransactionCountByHeight

This method is used to obtain the number of transactions in the block based on block height.

| Type | Template                                                                                      |
| ---- | --------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockTransactionCountByHeight","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height (default: -1)

##### Returns

- `result`:`int` - transactions count

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockTransactionCountByHeight","params":[-1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetBlockTransactionCountByHash

This method is used to obtain the number of transactions in the block based on block hash.

| Type | Template                                                                                     |
| ---- | -------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockTransactionCountByHash","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex

##### Returns

- `result`:`int` - transactions count

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockTransactionCountByHash","params":["0x0000004c0336e63f76e7bd2b7888514eff47b3528df67ca6ee95edb9dff79c00"],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetTransactionByBlockIndex

This method is used to obtain the transaction content based on block height or hash and transaction index.

| Type | Template                                                                                         |
| ---- | ------------------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getTransactionByBlockIndex","params":[string,int,int],"id":1}` |

##### Parameters

- `hash`:`string` - block hash
- `height`:`int` - block height (default: -1)
- `index`:`int` - transaction index, start with 0 (default: 0)

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getTransactionByBlockIndex","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922", -1, 1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "accountNonce": 0,
        "amount": 150000000,
        "from": "0x0000000000000000000000000000000000000000",
        "gasLimit": 0,
        "gasPrice": 0,
        "hash": "0x473ea3667d073491d5896a93fcf84d7dd822988d07482f21e7a875787539e62e",
        "payload": "",
        "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
    }
}
```
***

#### GetTransactionByBlockHeightAndIndex

This method is used to obtain the transaction content based on block height and transaction index.

| Type | Template                                                                                           |
| ---- | -------------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getTransactionByBlockHeightAndIndex","params":[int,int],"id":1}` |

##### Parameters

- `height`:`int` - block height (default: -1)
- `index`:`int` - transaction index, start with 0 (default: 0)

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getTransactionByBlockHeightAndIndex","params":[4202, 1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "accountNonce": 0,
        "amount": 150000000,
        "from": "0x0000000000000000000000000000000000000000",
        "gasLimit": 0,
        "gasPrice": 0,
        "hash": "0x473ea3667d073491d5896a93fcf84d7dd822988d07482f21e7a875787539e62e",
        "payload": "",
        "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
    }
}
```
***

#### GetTransactionByBlockHashAndIndex

This method is used to obtain the transaction content based on block hash and transaction index.

| Type | Template                                                                                            |
| ---- | --------------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getTransactionByBlockHashAndIndex","params":[string,int],"id":1}` |

##### Parameters

- `hash`:`string` - block hash
- `index`:`int` - transaction index, start with 0 (default: 0)

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getTransactionByBlockHashAndIndex","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922", 1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "accountNonce": 0,
        "amount": 150000000,
        "from": "0x0000000000000000000000000000000000000000",
        "gasLimit": 0,
        "gasPrice": 0,
        "hash": "0x473ea3667d073491d5896a93fcf84d7dd822988d07482f21e7a875787539e62e",
        "payload": "",
        "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
    }
}
```
***

#### GetReceiptByTxHash

This method is used to obtain the receipt contents based on transaction hash.

| Type | Template                                                                                |
| ---- | --------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getReceiptByTxHash","params":[string,string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex
- `abi`:`string` - the abi file of contract

##### Returns

- `contract`:`string` - contract address
- `failed`:`bool` - transaction executes successfully or not
- `poststate`:`string` - state trie root hash after transaction execution
- `result`:`string` - transaction result
- `totalFee`:`int` - transaction fee
- `txhash`:`string` - transaction hash
- `usedGas`:`int` - transaction gas

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getReceiptByTxHash","params":["0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff",""],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "contract": "0x",
        "failed": false,
        "poststate": "0xdd0b0fc6605bbb2e76b8c22ccd466ea5eaa1a80e4860fbdf971be58ded3d782b",
        "result": "0x",
        "totalFee": 1,
        "txhash": "0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff",
        "usedGas": 0
    }
}
```
***

#### GetTransactionsFrom

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                         |
| ---- | ------------------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getTransactionsFrom","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - from account
- `hexHash`:`string` - hex form of a block hash
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getTransactionsFrom","params":["0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1","",177],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasPrice" : 10,
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "amount" : 100000000,
            "payload" : "",
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "accountNonce" : 0,
            "gasLimit" : 21000,
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b"
         }
      }
   ]
```
***

#### GetTransactionsTo

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                       |
| ---- | ---------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getTransactionsTo","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - from account
- `hexHash`:`string` - hex form of a block hash
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getTransactionsTo","params":["0x75b86ef99c31bb858032d46bd533b18356c61aa1","",177],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasLimit" : 21000,
            "accountNonce" : 0,
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "amount" : 100000000,
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "gasPrice" : 10,
            "payload" : "",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b"
         }
      }
]
```
***


#### GetAccountTransactions

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                            |
| ---- | --------------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getAccountTransactions","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - from account
- `hexHash`:`string` - hex form of a block hash
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getAccountTransactions","params":["0x75b86ef99c31bb858032d46bd533b18356c61aa1","",177],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasLimit" : 21000,
            "accountNonce" : 0,
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "amount" : 100000000,
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "gasPrice" : 10,
            "payload" : "",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b"
         }
      }
]
```
***

#### GetBlockTransactions

This method returns transactions at specific height or block hash.

| Type | Template                                                                                   |
| ---- | ------------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockTransactions","params":[string ,uint64],"id":1}` |

##### Parameters

- `hexHash`:`string` - hex form of a block hash
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockTransactions","params":["",177],"id":1}' localhost:8037
```
- Result
```js
{
   "result" : [
      {
         "transaction 1" : {
            "amount" : 600000000,
            "gasPrice" : 0,
            "payload" : "",
            "gasLimit" : 0,
            "accountNonce" : 0,
            "to" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "from" : "0x0000000000000000000000000000000000000000",
            "hash" : "0xecc860869602e90b6f170e0106459fb243a637b49d5cf732b8f4526998bac1c5"
         }
      },
      {
         "transaction 2" : {
            "amount" : 100000000,
            "gasPrice" : 10,
            "payload" : "",
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b",
            "gasLimit" : 21000,
            "accountNonce" : 0
         }
      }
   ],
   "jsonrpc" : "2.0",
   "id" : 1
}
```
***

#### GetBlockTransactionsByHeight

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                   |
| ---- | ------------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockTransactionsByHeight","params":[uint64],"id":1}` |

##### Parameters

<!-- - `account`:`string` - from account -->
<!-- - `hexHash`:`string` - hex form of a block hash -->
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockTransactionsByHeight","params":[177],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasPrice" : 0,
            "to" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "accountNonce" : 0,
            "gasLimit" : 0,
            "hash" : "0xecc860869602e90b6f170e0106459fb243a637b49d5cf732b8f4526998bac1c5",
            "amount" : 600000000,
            "payload" : "",
            "from" : "0x0000000000000000000000000000000000000000"
         }
      },
      {
         "transaction 2" : {
            "payload" : "",
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "accountNonce" : 0,
            "gasPrice" : 10,
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b",
            "amount" : 100000000,
            "gasLimit" : 21000
         }
      }
   ]
```
***

#### GetBlockTransactionsByHash

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                 |
| ---- | ---------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"scdo_getBlockTransactionsByHash","params":[string],"id":1}` |

##### Parameters

<!-- - `account`:`string` - from account -->
<!-- - `hexHash`:`string` - hex form of a block hash -->
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"scdo_getBlockTransactionsByHash","params":["0x1220bd0253ac24aff8152ea19ad50e6724bac08f914630cea1e901ba19dbe021"],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasPrice" : 0,
            "to" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "accountNonce" : 0,
            "gasLimit" : 0,
            "hash" : "0xecc860869602e90b6f170e0106459fb243a637b49d5cf732b8f4526998bac1c5",
            "amount" : 600000000,
            "payload" : "",
            "from" : "0x0000000000000000000000000000000000000000"
         }
      },
      {
         "transaction 2" : {
            "payload" : "",
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "accountNonce" : 0,
            "gasPrice" : 10,
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b",
            "amount" : 100000000,
            "gasLimit" : 21000
         }
      }
   ]
```
***