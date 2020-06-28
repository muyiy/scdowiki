
| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [NodeInfo](#nodeinfo)   | &#x2713; |       | &#x2713; |         |
| [NodeStats](#nodestats) | &#x2713; |       | &#x2713; |         |

### monitor
node monitor.

***

#### NodeInfo

This method returns the node information of the node

| Type | Template                                                           |
| ---- | ------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"monitor_nodeInfo","params":[],"id":1}` |

##### Parameters

none

##### Returns

- `name`:`string` monitor name
- `node`:`string` node name
- `port`:`int` port
- `netVersion`:`string` node network version
- `protocol`:`string` node network protocol
- `api`:`string` monitor api
- `os`:`string` system os
- `os_v`:`string` system os architecture
- `client`:`string` client version
- `canUpdateHistory`:`bool` can update history?
- `shard`:`int` shard number

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"monitor_nodeInfo","params":[],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "name": "Test monitor",
        "node": "scdo node1",
        "port": 0,
        "netVersion": "1.0",
        "protocol": "1.0",
        "api": "No",
        "os": "windows",
        "os_v": "amd64",
        "client": "1.0",
        "canUpdateHistory": true,
        "shard": 1
    }
}
```
***

#### NodeStats

This method returns the information of the node

| Type | Template                                                            |
| ---- | ------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"monitor_nodeStats","params":[],"id":1}` |

##### Parameters

none

##### Returns

- `active`:`string` is node active？
- `syncing`:`string` is node syncing？
- `mining`:`int` is node mining?
- `peers`:`string` node peers number

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"monitor_nodeStats","params":[],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "active": true,
        "syncing": true,
        "mining": true,
        "peers": 0
    }
}
```
***
