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
- [scdo](api/scdo.md)

|Command                                                                     |   Full   |  Light   |  public  | private |
| --------------------------------------------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetInfo](api/scdo.md#getinfo)                                                         | &#x2713; |          | &#x2713; |         |
| [GetBalance](api/scdo.md#getbalance)                                                   | &#x2713; | &#x2713; | &#x2713; |         |
| [AddTx](api/scdo.md#addtx)                                                             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetAccountNonce](api/scdo.md#getaccountnonce)                                         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockHeight](api/scdo.md#getblockheight)                                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlock](api/scdo.md#getblock)                                                       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockByHash](api/scdo.md#getblockbyhash)                                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockByHeight](api/scdo.md#getblockbyheight)                                       | &#x2713; | &#x2713; | &#x2713; |         |
| [Call](api/scdo.md#call)                                                               | &#x2713; |          | &#x2713; |         |
| [GetLogs](api/scdo.md#getlogs)                                                         | &#x2713; |          | &#x2713; |         |
| [GetCode](api/scdo.md#getcode)                                                         | &#x2713; |          | &#x2713; |         |
| [GeneratePayload](api/scdo.md#generatepayload)                                         | &#x2713; |          | &#x2713; |         |
| [EstimateGas](api/scdo.md#estimategas)                                                 | &#x2713; |          | &#x2713; |         |
| [GetBlockTransactionCount](api/scdo.md#getblocktransactioncount)                       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionsFrom](api/scdo.md#gettransactionsfrom)                                 | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionsTo](api/scdo.md#gettransactionsto)                                     | &#x2713; | &#x2713; | &#x2713; |         |
| [GetAccountTransactions](api/scdo.md#getaccounttransactions)                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionsByHeight](api/scdo.md#getblocktransactionsbyheight)               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionsByHash](api/scdo.md#getblocktransactionsbyhash)                   | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactions](api/scdo.md#getblocktransactions)                               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionCountByHeight](api/scdo.md#getblocktransactioncountbyheight)       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionCountByHash](api/scdo.md#getblocktransactioncountbyhash)           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockIndex](api/scdo.md#gettransactionbyblockindex)                   | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockHeightAndIndex](api/scdo.md#gettransactionbyblockheightandindex) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockHashAndIndex](api/scdo.md#gettransactionbyblockhashandindex)     | &#x2713; | &#x2713; | &#x2713; |         |
| [GetReceiptByTxHash](api/scdo.md#getreceiptbytxhash)                                   | &#x2713; | &#x2713; | &#x2713; |         |

- [txpool](api/txpool.md)

| Command                                       |   Full   |  Light   |  public  | private |
| --------------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetTxPoolContent](api/txpool.md#gettxpoolcontent)         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTxPoolTxCount](api/txpool.md#gettxpooltxcount)         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPendingTxs](api/txpool.md#getpendingtxs)               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPendingDebts](api/txpool.md#getpendingdebts)           | &#x2713; |          | &#x2713; |         |
| [GetTransactionByHash](api/txpool.md#gettransactionbyhash) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetDebtByHash](api/txpool.md#getdebtbyhash)               | &#x2713; |          | &#x2713; |         |
| [GetGasPrice](api/txpool.md#getgasprice)                   | &#x2713; | &#x2713; | &#x2713; |         |

- [download](api/download.md)

| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [IsSyncing](api/download.md#issyncing) | &#x2713; |       | &#x2713; |         |
| [GetStatus](api/download.md#getstatus) | &#x2713; |       | &#x2713; |         |

- [network](api/network.md)


| Command                                   |   Full   |  Light   |  public  | private |
| ----------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetPeersInfo](api/network.md#getpeersinfo)             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPeerCount](api/network.md#getpeercount)             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetNetVersion](api/network.md#getnetversion)           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetProtocolVersion](api/network.md#getprotocolversion) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetNetworkID](api/network.md#getnetworkid)             | &#x2713; | &#x2713; | &#x2713; |         |
| [IsListening](api/network.md#islistening)               | &#x2713; | &#x2713; | &#x2713; |         |

- [miner](api/miner.md)

| Command                     |   Full   | Light | public | private  |
| --------------------------- |:--------:|:-----:|:------:|:--------:|
| [Start](api/miner.md#start)             | &#x2713; |       |        | &#x2713; |
| [Stop](api/miner.md#stop)               | &#x2713; |       |        | &#x2713; |
| [Status](api/miner.md#status)           | &#x2713; |       |        | &#x2713; |
| [GetCoinbase](api/miner.md#getcoinbase) | &#x2713; |       |        | &#x2713; |
| [GetTarget](api/miner.md#gettarget)     | &#x2713; |       |        | &#x2713; |
| [GetWork](api/miner.md#getwork)         | &#x2713; |       |        | &#x2713; |
| [SetThreads](api/miner.md#setthreads)   | &#x2713; |       |        | &#x2713; |
| [SetCoinbase](api/miner.md#setcoinbase) | &#x2713; |       |        | &#x2713; |
| [GetThreads](api/miner.md#getthreads)   | &#x2713; |       |        | &#x2713; |


- [debug](api/debug.md#)

| Command                   |   Full   | Light | public | private  |
| ------------------------- |:--------:|:-----:|:------:|:--------:|
| [PrintBlock](api/debug.md#printblock) | &#x2713; |       |        | &#x2713; |
| [DumpHeap](api/debug.md#dumpheap)     | &#x2713; |       |        | &#x2713; |
| [GetTPS](api/debug.md#gettps)         | &#x2713; |       |        | &#x2713; |

- [monitor](api/monitor.md)

| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [NodeInfo](api/monitor.md#nodeinfo)   | &#x2713; |       | &#x2713; |         |
| [NodeStats](api/monitor.md#nodestats) | &#x2713; |       | &#x2713; |         |













