
| Command                                   |   Full   |  Light   |  public  | private |
| ----------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetPeersInfo](#getpeersinfo)             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPeerCount](#getpeercount)             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetNetVersion](#getnetversion)           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetProtocolVersion](#getprotocolversion) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetNetworkID](#getnetworkid)             | &#x2713; | &#x2713; | &#x2713; |         |
| [IsListening](#islistening)               | &#x2713; | &#x2713; | &#x2713; |         |

### network

RPC collection provided for internal inquiry of network node information.

***

#### GetPeersInfo

This method returns the information of peer nodes.

| Type | Template                                                               |
| ---- | ---------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getPeersInfo","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `id`:`string` - node ID
- `caps`:`array` - peer node protocol and version array
- `network`:`struct` - network access address collection
  - `localAddress`:`string` - local address
  - `remoteAddress`:`string` - remote address
- `protocols`:`map` - node collection, key is the node name
  - `version`:`int` - node protocal
  - `difficulty`:`big.Int` - node difficulty
  - `head`:`string` - current block hash of the node
- `shard`:`uint` - shard id of the node
##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getPeersInfo","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
        {
            "id": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
            "caps": [
                "lightscdo_1/1",
                "lightscdo_2/1",
                "scdo/1"
            ],
            "network": {
                "localAddress": "127.0.0.1:54652",
                "remoteAddress": "127.0.0.1:8058"
            },
            "protocols": {
                "lightscdo_1": {
                    "version": 1,
                    "difficulty": 54618694483,
                    "head": "0000040c0c7af9b83736210e0f177998e61d2ec8b314fd2d4f49b8a11c4a28b7"
                },
                "lightscdo_2": {
                    "version": 1,
                    "difficulty": 2395409154,
                    "head": "0000030e2940702b853faa83f01cf34d7324de11ad0e52b4f33851c41e41ecf0"
                },
                "scdo": {
                    "version": 1,
                    "difficulty": 2395409154,
                    "head": "0000030e2940702b853faa83f01cf34d7324de11ad0e52b4f33851c41e41ecf0"
                }
            },
            "shard": 2
        }
    ]
}
```
***

#### GetPeerCount

This method returns the number of peer nodes.

| Type | Template                                                               |
| ---- | ---------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getPeerCount","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`int` - peer number of node

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getPeerCount","params":[],"id":2}' localhost:8037
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

#### GetNetVersion

This method returns the network version.

| Type | Template                                                                |
| ---- | ----------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getNetVersion","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - version number

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getNetVersion","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1.0
}
```
***

#### GetProtocolVersion

This method returns the protocol version.

| Type | Template                                                                     |
| ---- | ---------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getProtocolVersion","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`int` - version number

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getProtocolVersion","params":[],"id":2}' localhost:8037
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

#### GetNetworkID

This method returns the network id.

| Type | Template                                                               |
| ---- | ---------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getNetworkID","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - network id

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getNetworkID","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "scdo"
}
```
***

#### IsListening

This method returns whether the node network is listening or not.

| Type | Template                                                              |
| ---- | --------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_isListening","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`bool` - listening status

##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_isListening","params":[],"id":2}' localhost:8037
```
- Result
```js
{
   "id" : 2,
   "jsonrpc" : "2.0",
   "result" : true
}
```
***