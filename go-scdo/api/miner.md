| Command                     |   Full   | Light | public | private  |
| --------------------------- |:--------:|:-----:|:------:|:--------:|
| [Start](#start)             | &#x2713; |       |        | &#x2713; |
| [Stop](#stop)               | &#x2713; |       |        | &#x2713; |
| [Status](#status)           | &#x2713; |       |        | &#x2713; |
| [GetCoinbase](#getcoinbase) | &#x2713; |       |        | &#x2713; |
| [GetTarget](#gettarget)     | &#x2713; |       |        | &#x2713; |
| [GetWork](#getwork)         | &#x2713; |       |        | &#x2713; |
| [SetThreads](#setthreads)   | &#x2713; |       |        | &#x2713; |
| [SetCoinbase](#setcoinbase) | &#x2713; |       |        | &#x2713; |
| [GetThreads](#getthreads)   | &#x2713; |       |        | &#x2713; |

### miner
RPC collection provided for internal inquiry of miner information.
***

#### Start

This method starts the miner with an input number of threads.

| Type | Template                                                         |
| ---- | ---------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_start","params":[int],"id":2}` |

##### Parameters

- `threads`:`int` - number of threads

##### Returns

- `result`:`bool` - start result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_start","params":[2],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### Stop

This method stops the miner.

| Type | Template                                                     |
| ---- | ------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"miner_stop","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`bool` - stop result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_stop","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### Status

This method returns the miner status.

| Type | Template                                                       |
| ---- | -------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_status","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - miner status

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_status","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "running"
}
```
***

#### GetCoinbase

This method is used to obtain the node coinbase.

| Type | Template                                                            |
| ---- | ------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_getCoinbase","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - coinbase

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_getCoinbase","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
}
```
***

#### GetTarget

This method is used to obtain current SPOW mining difficulty.

| Type | Template                                                          |
| ---- | ----------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_getTarget","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - current SPOW mining difficulty

##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_getTarget","params":[],"id":2}' localhost:8037
```
- Result
```js
{
   "jsonrpc" : "2.0",
   "id" : 2,
   "result" : "569762050"
}
```
***


#### GetWork

This method return miner current mining task.

| Type | Template                                                        |
| ---- | --------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_getWork","params":[],"id":2}` |

##### Parameters

- `threads`:`int` - miner threads

##### Returns

- `result`:`bool` - SetThreads result

##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_getWork","params":[4],"id":2}' localhost:8037
```
- Result
```js
{
   "result" : {
      "debts" : null,
      "txs" : [
         {
            "Data" : {
               "GasPrice" : 0,
               "From" : "0x0000000000000000000000000000000000000000",
               "Type" : 1,
               "Timestamp" : 1580171186,
               "Payload" : "",
               "AccountNonce" : 0,
               "Amount" : 600000000,
               "GasLimit" : 0,
               "To" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1"
            },
            "Signature" : {
               "Sig" : ""
            },
            "Hash" : "0x3a3aa0d94085291262dbd7a177cd451d694618a6315692a68cf22cc6db98a89f"
         }
      ],
      "receipts" : [
         {
            "TxHash" : "0x3a3aa0d94085291262dbd7a177cd451d694618a6315692a68cf22cc6db98a89f",
            "TotalFee" : 0,
            "Result" : null,
            "PostState" : "0x09976f41a4a82d87a60450f5701264aca52544b89731f86707a7f970e01b3df8",
            "Logs" : null,
            "UsedGas" : 0,
            "Failed" : false,
            "ContractAddress" : null
         }
      ],
      "header" : {
         "Witness" : null,
         "ReceiptHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
         "DebtHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
         "SecondWitness" : null,
         "PreviousBlockHash" : "0xe84c9437d787e93676f891d9da54056272a8b460f7b057ea6a343bc3089f6c12",
         "CreateTimestamp" : 1580171186,
         "TxHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
         "Creator" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
         "TxDebtHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
         "Difficulty" : 8769846,
         "ExtraData" : null,
         "Height" : 3021,
         "StateHash" : "0x09976f41a4a82d87a60450f5701264aca52544b89731f86707a7f970e01b3df8",
         "Consensus" : 0
      },
      "coinbase" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1"
   },
   "jsonrpc" : "2.0",
   "id" : 2
}
```
***


#### SetThreads

This method is used to set the threads of miner consensus.

| Type | Template                                                           |
| ---- | ------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"miner_setThreads","params":[],"id":2}` |

##### Parameters

- `threads`:`int` - miner threads

##### Returns

- `result`:`bool` - SetThreads result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_setThreads","params":[4],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### SetCoinbase

This method is used to set the coinbase

| Type | Template                                                                    |
| ---- | --------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_setCoinbase","params":["string"],"id":2}` |

##### Parameters

- `coinbase`:`string` coinbase of the miner

##### Returns

- `result`:`bool` - SetCoinbase result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_setCoinbase","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### GetThreads

This method is used to get the threads of miner consensus.

| Type | Template                                                           |
| ---- | ------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"miner_getThreads","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`int` - miner threads

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_getThreads","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 2
}
```
***