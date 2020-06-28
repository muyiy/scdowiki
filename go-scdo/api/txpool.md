
| Command                                       |   Full   |  Light   |  public  | private |
| --------------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetTxPoolContent](#gettxpoolcontent)         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTxPoolTxCount](#gettxpooltxcount)         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPendingTxs](#getpendingtxs)               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPendingDebts](#getpendingdebts)           | &#x2713; |          | &#x2713; |         |
| [GetTransactionByHash](#gettransactionbyhash) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetDebtByHash](#getdebtbyhash)               | &#x2713; |          | &#x2713; |         |
| [GetGasPrice](#getgasprice)                   | &#x2713; | &#x2713; | &#x2713; |         |

### txpool
RPC collection provided for internal use for transaction pool inquiry manipulation.
***

#### GetTransactionByHash

This method returns transaction information by hash.

| Type | Template                                                                            |
| ---- | ----------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getTransactionByHash","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex

##### Returns

- `blockHash`:`string` - block hash
- `blockHeight`:`int` - block height
- `status`:`string` - transaction status
- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `signature`:`string` - transaction signature
- `txIndex`:`int` - transaction index in block

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTransactionByHash","params":["0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff"],"id":1}' localhost:8037
```
- Result

```js
{
   "jsonrpc": "2.0",
   "id": 1,
   "result": {
      "blockHash": "0x702dc20ce8379ba340aff4a05d37faa818542032c3326832237a8c4f90a6ff2d",
      "blockHeight": 1733757,
      "status": "block",
      "transaction": {
         "accountNonce": 64,
         "amount": 10,
         "from": "0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1",
         "gasLimit": 21000,
         "gasPrice": 1,
         "hash": "0xa56fc9d8fb292c989c61be57d3a2e77902d68331d19cfb689e491574c679b7a0",
         "payload": "",
         "signature": {
            "Sig": "3a/HhtAao9QiLmGkjgcv2tRSsvMxx1myWJoCVYpaJ64T49rYmYWWpE0JCAjYVqPkK8t4V88C+0VTLKkBfd68+wA="
         },
         "to": "0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1"
      },
      "txIndex": 1
   }
}
```
***

#### GetDebtByHash

This method is used to obtain the debt contents based on debt hash.

| Type | Template                                                                     |
| ---- | ---------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getDebtByHash","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - debt hash value in hex

##### Returns

- `blockHash`:`string` - block hash of the debt on
- `blockHeight`:`int64` - block height of the debt on
- `debt`:`json` - debt json
  - `Hash`:`string` - debt hash
  - `Data`:`json` - debt data
    - `TxHash`:`string` - txhash in debt
    - `From`:`string` - address of the sender
    - `Nonce`: `uint64` - nonce of From address
    - `Account`:`string` - debt account
    - `Amount`:`int64` - debt amount
    - `Price`:`int64` - debt price
    - `Code`:`string` - debt contract code
- `debtIndex`:`int` - debt index of the block debts
- `status`:`string` - debt status

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getDebtByHash","params":["0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e"],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "blockHash": "0x000001fb7817c8d9eeaa9bbed6670f8db62b605ad174f561e74afc60ac18c97b",
        "blockHeight": 170,
        "debt": {
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
        },
        "debtIndex": 0,
        "status": "block"
    }
}
```
***
#### GetGasPrice

This method returns the tx gas price.

| Type | Template                                                                   |
| ---- | -------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getGasPrice","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex

##### Returns

- `gasPrice`:`Int` - transaction gas price


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getGasPrice","params":["0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b"],"id":1}' localhost:8037
```
- Result
```js
{
	"gasPrice": 10
}
```
Or (if transaction is not found)
```js
{
	"error": "the transaction not found"
}
```
***

#### GetTxPoolContent

This method is used to obtain the transaction pool content.

| Type | Template                                                                  |
| ---- | ------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getTxPoolContent","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`string` - transaction timestamp
- `GasPrice`:`int64` - transaction gas price
- `GasLimit`:`int64` - transaction gas limit

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTxPoolContent","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "0x3b691130ec4166bfc9ec7240217fc8d08903cf21": [
            {
                "accountNonce": 102,
                "amount": 1,
                "from": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                "gasLimit": 21000,
                "gasPrice": 10,
                "hash": "0x1a4eb0f6754ef9b973c084f9b285296d616bd36cb9e3707e743d38db9edc7e8f",
                "payload": "",
                "to": "0x2a87b6504cd00af95a83b9887112016a2a991cf1"
            }
        ]
    }
}
```
***

#### GetTxPoolTxCount

This method is used to obtain the number of transactions in the transaction pool.

| Type | Template                                                                  |
| ---- | ------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getTxPoolTxCount","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`uint64` - number of transactions

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTxPoolTxCount","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1
}
```
***

#### GetPendingTransactions

This method is used to obtain pending transactions in the transaction pool.

| Type | Template                                                                        |
| ---- | ------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getPendingTransactions","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`string` - transaction timestamp
- `fee`:`int` - transaction fee

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getPendingTransactions","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
              	{
              		"accountNonce": 6,
              		"amount": 10000,
              		"fee": 1,
              		"from": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
              		"hash": "0x4ad5843af174d32e31b54ef81ddcbfeec43f4eb5d01885dfe9828f9ce907fb80",
              		"payload": "",
              		"timestamp": 0,
              		"to": "0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71"
              	}
              ]
}
```
***

#### GetPendingDebts

This method is used to obtain pending transactions in the transaction pool.

| Type | Template                                                                 |
| ---- | ------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getPendingDebts","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `Data`:`json` - debt data
	- `Account`:`array` - debt account
	- `Amount`:`int64` - debt amount
	- `Code`:`string` - debt code
	- `Fee`:`int64` - debt fee
	- `Shard`:`int` - shard number of scdo node where debts on
	- `TxHash`:`string` - txhash in debt
- `Hash`:`string` - debts hash

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getPendingDebts","params":[],"id":2}' localhost:8037
```
- Result

```js
[
        {
                "Data": {
                        "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                        "Amount": 10000,
                        "Code": "",
                        "Fee": 0,
                        "Shard": 2,
                        "TxHash": "0x049305964eac1c62b19f0a6a0841b1d24683c4c4f9a3f23c69c87dcca9ec3e28"
                },
                "Hash": "0xdcf8489c27e934c3f289c4a1d843b86dbd3445e8943903613ce640d7fb043e87"
        }
]
```
***