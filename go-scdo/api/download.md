| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [IsSyncing](#issyncing) | &#x2713; |       | &#x2713; |         |
| [GetStatus](#getstatus) | &#x2713; |       | &#x2713; |         |

### download
RPC collection provided for internal inquiry of blockchain node synchronization state.

***

#### GetStatus

This method returns synchronization information.

| Type | Template                                                             |
| ---- | -------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"download_getStatus","params":[],"id":2}` |

##### Parameters
none

##### Returns

- `Status`:`string` - synchronization state
- `Duration`:`string` - synchronization duration (seconds)
- `StartNum`:`uint64` - synchronization initial block height
- `Amount`:`uint64` - synchronization value
- `Downloaded`:`uint64` - Synchronization number of times

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"download_getStatus","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "Status": "NotSyncing",
        "Duration": "",
        "StartNum": 0,
        "Amount": 0,
        "Downloaded": 0
    }
}
```
***

#### IsSyncing

This method returns the synchronization status.

| Type | Template                                                             |
| ---- | -------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"download_isSyncing","params":[],"id":2}` |

##### Parameters
none

##### Returns

- `result`:`bool` - synchronization state

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"download_isSyncing","params":[],"id":2}' localhost:8037
```
- Result

```js
{
	"jsonrpc":"2.0",
	"id":2,
	"result":false
}
```
***