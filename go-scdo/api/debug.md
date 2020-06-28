| Command                   |   Full   | Light | public | private  |
| ------------------------- |:--------:|:-----:|:------:|:--------:|
| [PrintBlock](#printblock) | &#x2713; |       |        | &#x2713; |
| [DumpHeap](#dumpheap)     | &#x2713; |       |        | &#x2713; |
| [GetTPS](#gettps)         | &#x2713; |       |        | &#x2713; |


### debug
RPC collection provided for internal debugging.
***

#### PrintBlock

This method is used to print block information in dump format based on block height.

| Type | Template                                                                |
| ---- | ----------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"debug_printBlock","params":[int64],"id":2}` |

##### Parameters

- `height`:`int64` - block height

##### Returns

- `HeaderHash`:`string` - block header hash
- `Header`:`json` - block header
  - `PreviousBlockHash`:`string` - previous block hash
  - `Creator`:`string` - block creator
  - `StateHash`:`string` - state hash
  - `TxHash`:`string` - transactions hash
  - `ReceiptHash`:`string` - receipts hash
  - `TxDebtHash`:`string` - transaction debts hash
  - `DebtHash`:`string` - debts hash
  - `Difficulty`:`big.Int` - block td
  - `Height`:`uint64` - block height
  - `CreateTimestamp`:`big.Int` - create timestamp
  - `Witness`:`string` - block nonce
  - `Consensus`:`int` - 0 for POW consensus
  - `ExtraData`:`string` - extra data
- `Transactions`:`array` - transactions on block
  - `Hash`:`string` - transaction hash
  - `Data`:`string` - transaction data
    - `Type`:`int` - transaction type, 0 for regular type, 1 for reward type
    - `From`:`string` - amount sender
    - `To`:`string` - amount receiver
    - `Amount`:`int64` - transaction amount
    - `AccountNonce`:`int64` - account nonce
    - `GasPrice`:`int64` - transaction gas price
    - `GasLimit`:`int64` - maximum gas for contract creation/execution
    - `Timestamp`:`int64` - transaction timestamp
    - `Payload`:`string` - payload
    - `Signature`:`json` - transaction signature json
      - `Sig`:`string` - transaction sig
- `Debts`:`array` - dump format of block information
  - `Hash`:`string` - debts hash
  - `Data`:`json` - debts data
    - `TxHash`:`string` - txhash in debt
    - `From`:`string` - sender address
    - `Nonce`:`int64` - sender nonce
    - `Account`:`string` - debt account
    - `Amount`:`int64` - debt amount
    - `Price`:`int64` - debt gas price
    - `Code`:`string` - debt code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"debug_printBlock","params":[10368],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "HeaderHash": "0x000001a8946d75258f9e269d516e797779ca6bd4b190c701f81456c60958c688",
        "Header": {
            "PreviousBlockHash": "0x000001f2ba4bc08c6a39fb35fa193698f35066c6ca14ca773b944eae25a6c360",
            "Creator": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
            "StateHash": "0x875cd1618715a8414eb48f957b8a92b70699a9b3a94848d92da2fa278494ecc3",
            "TxHash": "0x390b401fa139861dcc7b7d78f18b043672a729b6d688b8cba38946b2b4114bb9",
            "ReceiptHash": "0x62db1441782a734fa65ee8f0678a8dd028fc813a11e4784ad24b596f5a071f01",
            "TxDebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "DebtHash": "0x5b240a1f3d6369489307fee52be9bc759312f873bde832bda975ee774ecacfaa",
            "Difficulty": 6348338,
            "Height": 1112,
            "CreateTimestamp": 1539147474,
            "Nonce": 16880251435180988161,
            "ExtraData": ""
        },
        "Transactions": [
            {
                "Hash": "0x8bb8afe4222ed759af503ab95417015321b4992c7913b440f1be47536929d3b4",
                "Data": {
                    "From": "0x0000000000000000000000000000000000000000",
                    "To": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 150000000,
                    "AccountNonce": 0,
                    "Fee": 0,
                    "Timestamp": 1539147474,
                    "Payload": ""
                },
                "Signature": {
                    "Sig": ""
                }
            }
        ],
        "Debts": [
            {
                "Hash": "0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e",
                "Data": {
                    "TxHash": "0x58752f8aeb2c69dd2c32059d3ad8b2d3d860c6d92aa2b3b30ff985e564f60fae",
                    "Shard": 2,
                    "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 10000,
                    "Fee": 0,
                    "Code": ""
                }
            }
        ]
    }
}
```
***


#### DumpHeap

This method dump heap for profiling and returns the file path.

| Type | Template                                                         |
| ---- | ---------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"debug_dumpHeap","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` file path

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"debug_dumpHeap","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc":"2.0",
    "id":2,
    "result":"C:\Users\dell-2\.scdo\heap.dump"
}
```
***

#### GetTPS

This method returns TPS of scdo node.

| Type | Template                                                       |
| ---- | -------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"debug_getTPS","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `StartHeight`:`int64` start height
- `EndHeight`:`int64` end height
- `Count`:`int` tps
- `Duration`:`int` elapsed time from start height to end height

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"debug_getTPS","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "StartHeight": 13929,
        "EndHeight": 13941,
        "Count": 0,
        "Duration": 166
    }
}
```
***