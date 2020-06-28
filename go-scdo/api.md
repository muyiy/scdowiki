# SCDO JSON-RPC

## Curl 

To use a curl command below, run a shard 1 node locally serving http at 8037[!!!]. The curl options below might return a response where the node complains about the content type, this is because the --data option sets the content type to application/x-www-form-urlencoded .

## Request Types

| Type           | Supported? |
| -------------- |:----------:|
| JSON-RPC 1.0   |  &#x2713;  |
| JSON-RPC 2.0   |  &#x2713;  |
| Batch Requests |  &#x2713;  |
| HTTP           |  &#x2713;  |
| WS             |  &#x2713;  |


## Ports
Default port:

| Client | Type        | Address               |
| ------ | ----------- |:--------------------- |
| Go     | jsonrpc-2.0 | http://localhost:8027 |
| Go     | http        | http://localhost:8037 |
| Go     | websocket   | http://localhost:8047 |

## Namespaces
- `scdo`:node data manipulation and procurement / acquisition
- `txpool`:transaction pool management
- `download`:RPC collection provided for internal inquiry of blockchain node synchronization state.
- `network`:connection management
- `miner`:miner manipulation
- `debug`:node debugging
- `monitor`:node monitor

## Table of Contents
- [scdo](#scdo)
- [txpool](#txpool)
- [download](#download)
- [network](#network)
- [miner](#miner)
- [debug](#debug)
- [monitor](#monitor)

| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [NodeInfo](api/monitor/#nodeinfo)   | &#x2713; |       | &#x2713; |         |
| [NodeStats](#nodestats) | &#x2713; |       | &#x2713; |         |













