# Transactions

Two basic concerns of sending any transaction are balance and nonce. The balance of the sender must be able to cover both the ammount and the transaction fee (minimal .0021 SCDO for same-shard, .0063 SCDO for cross-shard). A limit for transaction fee can be set by the gasLimit and gasPrice of the transaction data structure (the total is gasLimit*gasPrice). The nonce must be the newest nonce. Sending multiple transactions with different nonces could cause some transactions to be lost forever in case transactions with higher nonce is blocked first. It is recommended to send 1 transaction at a time.

View address balance and nonce

```
$ ./client getbalance --account 1Sfe11f81e3da032dd3d0728795d90620ec161ecf1 -a 198.251.69.156:8027
{
	"Account": "1Sfe11f81e3da032dd3d0728795d90620ec161ecf1",
	"Balance": 0
}

$ ./client getnonce --account 1Sfe11f81e3da032dd3d0728795d90620ec161ecf1 -a 198.251.69.156:8027
0
```

Send transaction with keyfile. Transaction hash is `0x4dec...`. This hash is needed for transaction confirmation.

```
$ ./client sendtx --from mykey --amount 10 --to 1S2511c163cb5c48d3a3265b1ec3b29c0aeab936c1  
Please input your key file password: 
sendtx without setting nonce, GetAccountNonce 4
account: 1S36aa4d4f192e802217fc0bad6860e75ec719ea31, transaction nonce: 4
transaction sent successfully
{
	"Hash": "0x4decbc9f0f91c2ec1fc3b0a6c0ce7ebab5d540a9b678d5ac624004458247d442",
	"Data": {
		"Type": 0,
		"From": "1S36aa4d4f192e802217fc0bad6860e75ec719ea31",
		"To": "1S2511c163cb5c48d3a3265b1ec3b29c0aeab936c1",
		"Amount": 10,
		"AccountNonce": 4,
		"GasPrice": 10,
		"GasLimit": 21000,
		"Timestamp": 0,
		"Payload": ""
	},
	"Signature": {
		"Sig": "IEimXGSL00IncZ8UE1o8Mlly+KNaCABlNUI4XLMLyshtu7Tz63l8qsOXz5VkvBpHuGwdYeXYkJOA9B6cSs1rXwA="
	}
}
```
Confirm transaction by hash or receipt.
```
$ ./client gettxbyhash --hash 0x4decbc9f0f91c2ec1fc3b0a6c0ce7ebab5d540a9b678d5ac624004458247d442
{
	"blockHash": "0x2fe96d0f7a3acfdb45da948b8a08f93d4b8f4a560071c078d2bf2c8b5be26097",
	"blockHeight": 2918999,
	"status": "block",
	"transaction": {
		"accountNonce": 4,
		"amount": 10,
		"from": "1S36aa4d4f192e802217fc0bad6860e75ec719ea31",
		"gasLimit": 21000,
		"gasPrice": 10,
		"hash": "0x4decbc9f0f91c2ec1fc3b0a6c0ce7ebab5d540a9b678d5ac624004458247d442",
		"payload": "",
		"signature": {
			"Sig": "IEimXGSL00IncZ8UE1o8Mlly+KNaCABlNUI4XLMLyshtu7Tz63l8qsOXz5VkvBpHuGwdYeXYkJOA9B6cSs1rXwA="
		},
		"to": "1S2511c163cb5c48d3a3265b1ec3b29c0aeab936c1"
	},
	"txIndex": 1
}

$ ./client getreceipt --hash 0x4decbc9f0f91c2ec1fc3b0a6c0ce7ebab5d540a9b678d5ac624004458247d442
{
	"contract": "0x",
	"failed": false,
	"poststate": "0x8351d56d0766bb7e341b5da678aab474bfbfd90719288cfe5abbf81050e5ece0",
	"result": "0x",
	"totalFee": 210000,
	"txhash": "0x4decbc9f0f91c2ec1fc3b0a6c0ce7ebab5d540a9b678d5ac624004458247d442",
	"usedGas": 21000
}
```
Sending a cross-shard transaction. The transaction hash is `0x38d4...` and the debt transaction hash is `0x376c...`. Theses hashes will be used for confirmation of this transaction.
```
$ ./client sendtx --from mykey --amount 10 --to 3Sf2ffd6f938aef7c4fef71882fb813efc92ed79d1
Please input your key file password: 
sendtx without setting nonce, GetAccountNonce 0
account: 1S36aa4d4f192e802217fc0bad6860e75ec719ea31, transaction nonce: 0
transaction sent successfully
{
	"Hash": "0x38d4b0f9c72eaf950337261f5a87649b6ade1b617816a543c1742decdcc68839",
	"Data": {
		"Type": 0,
		"From": "1S36aa4d4f192e802217fc0bad6860e75ec719ea31",
		"To": "3Sf2ffd6f938aef7c4fef71882fb813efc92ed79d1",
		"Amount": 10,
		"AccountNonce": 0,
		"GasPrice": 10,
		"GasLimit": 63000,
		"Timestamp": 0,
		"Payload": ""
	},
	"Signature": {
		"Sig": "PeUrJkJEBvvGnRLfAUN+5KVVsBp2vsrwNF7LrLu/qRgLM/zfRhX9ehy9erroppNlvrM59R/b2af3Ao6tviUq/AE="
	}
}

It is a cross shard transaction, its debt is:
{
	"Hash": "0x376ceca09e3cb06b84ad574f8b3adc260a2683e997d950955c97c17c0786edb3",
	"Data": {
		"TxHash": "0x38d4b0f9c72eaf950337261f5a87649b6ade1b617816a543c1742decdcc68839",
		"From": "1S36aa4d4f192e802217fc0bad6860e75ec719ea31",
		"Nonce": 0,
		"Account": "3Sf2ffd6f938aef7c4fef71882fb813efc92ed79d1",
		"Amount": 10,
		"Price": 10,
		"Code": ""
	}
}
```
Confirm cross-shard transaction on sender chain after 14 seconds.
```
./client gettxbyhash --hash 0x38d4b0f9c72eaf950337261f5a87649b6ade1b617816a543c1742decdcc68839
{
	"blockHash": "0xf35f59d5ced9c3c25e49b450272bd9578082f85801ce35d0cd3ce7dab1111973",
	"blockHeight": 2916759,
	"debt": {
		"Data": {
			"Account": "3Sf2ffd6f938aef7c4fef71882fb813efc92ed79d1",
			"Amount": 10,
			"Code": "",
			"From": "1S36aa4d4f192e802217fc0bad6860e75ec719ea31",
			"Nonce": 0,
			"Price": 10,
			"TxHash": "0x38d4b0f9c72eaf950337261f5a87649b6ade1b617816a543c1742decdcc68839"
		},
		"Hash": "0x376ceca09e3cb06b84ad574f8b3adc260a2683e997d950955c97c17c0786edb3"
	},
	"status": "block",
	"transaction": {
		"accountNonce": 0,
		"amount": 10,
		"from": "1S36aa4d4f192e802217fc0bad6860e75ec719ea31",
		"gasLimit": 63000,
		"gasPrice": 10,
		"hash": "0x38d4b0f9c72eaf950337261f5a87649b6ade1b617816a543c1742decdcc68839",
		"payload": "",
		"signature": {
			"Sig": "PeUrJkJEBvvGnRLfAUN+5KVVsBp2vsrwNF7LrLu/qRgLM/zfRhX9ehy9erroppNlvrM59R/b2af3Ao6tviUq/AE="
		},
		"to": "3Sf2ffd6f938aef7c4fef71882fb813efc92ed79d1"
	},
	"txIndex": 1
}
```
Confirm cross-shard transaction on receiver chain after 120 depth past (in this case 2916759 + 120 = 2916879) on the sender chain. A local shard 3 node needs to mine with default port 8029 for this demo to work.
```
$ ./client getdebtbyhash --hash 0x376ceca09e3cb06b84ad574f8b3adc260a2683e997d950955c97c17c0786edb3 -a 127.0.0.1:8029
{
	"blockHash": "0x33aa6086ef3e68cca58e2019139e74ce1c3964aa997c7f298a2611beaab851f3",
	"blockHeight": 2917105,
	"debt": {
		"Data": {
			"Account": "3Sf2ffd6f938aef7c4fef71882fb813efc92ed79d1",
			"Amount": 10,
			"Code": "",
			"From": "1S36aa4d4f192e802217fc0bad6860e75ec719ea31",
			"Nonce": 0,
			"Price": 10,
			"TxHash": "0x38d4b0f9c72eaf950337261f5a87649b6ade1b617816a543c1742decdcc68839"
		},
		"Hash": "0x376ceca09e3cb06b84ad574f8b3adc260a2683e997d950955c97c17c0786edb3"
	},
	"debtIndex": 0,
	"status": "block"
}
```

\* As mentioned in [shard tutorial](shard.md), it is good practice to wait for block depth for same-shard transaction or cross-shard debt transaction.

# Curl 

All remote client commands ultimately calls scdo's API: getinfo, getnonce, getbalance, etc. Another way to test these APIs is through curl commands. This section of go-scdo will go through definitions and purposes of these APIs and how to use them through curl. The [`scdo.js`](scdo.js/get.md) tool's rpc module covers all the APIs listed below, all client capabilities and more.  

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
| Go     | jsonrpc-2.0 | http://localhost:8026-8029 |
| Go     | http        | http://localhost:8036-8039 |
| Go     | websocket   | http://localhost:8046-8049 |

\* Last digit of port 6-9 matches shard 4, 1, 2, 3 nodes (ex: shard 1 8027,8037,8047; shard 3 8029,8039,8049).

## Namespaces
- `scdo`:node data manipulation and procurement / acquisition
- `txpool`:transaction pool management
- `download`:RPC collection provided for internal inquiry of blockchain node synchronization state.
- `network`:connection management
- `miner`:miner manipulation
- `debug`:node debugging
- `monitor`:node monitor

# Reference Links

## [scdo](api/scdo.md)

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

## [txpool](api/txpool.md)

| Command                                       |   Full   |  Light   |  public  | private |
| --------------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetTxPoolContent](api/txpool.md#gettxpoolcontent)         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTxPoolTxCount](api/txpool.md#gettxpooltxcount)         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPendingTxs](api/txpool.md#getpendingtxs)               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPendingDebts](api/txpool.md#getpendingdebts)           | &#x2713; |          | &#x2713; |         |
| [GetTransactionByHash](api/txpool.md#gettransactionbyhash) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetDebtByHash](api/txpool.md#getdebtbyhash)               | &#x2713; |          | &#x2713; |         |
| [GetGasPrice](api/txpool.md#getgasprice)                   | &#x2713; | &#x2713; | &#x2713; |         |

## [download](api/download.md)

| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [IsSyncing](api/download.md#issyncing) | &#x2713; |       | &#x2713; |         |
| [GetStatus](api/download.md#getstatus) | &#x2713; |       | &#x2713; |         |

## [network](api/network.md)


| Command                                   |   Full   |  Light   |  public  | private |
| ----------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetPeersInfo](api/network.md#getpeersinfo)             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPeerCount](api/network.md#getpeercount)             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetNetVersion](api/network.md#getnetversion)           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetProtocolVersion](api/network.md#getprotocolversion) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetNetworkID](api/network.md#getnetworkid)             | &#x2713; | &#x2713; | &#x2713; |         |
| [IsListening](api/network.md#islistening)               | &#x2713; | &#x2713; | &#x2713; |         |

## [miner](api/miner.md)

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


## [debug](api/debug.md#)

| Command                   |   Full   | Light | public | private  |
| ------------------------- |:--------:|:-----:|:------:|:--------:|
| [PrintBlock](api/debug.md#printblock) | &#x2713; |       |        | &#x2713; |
| [DumpHeap](api/debug.md#dumpheap)     | &#x2713; |       |        | &#x2713; |
| [GetTPS](api/debug.md#gettps)         | &#x2713; |       |        | &#x2713; |

## [monitor](api/monitor.md)

| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [NodeInfo](api/monitor.md#nodeinfo)   | &#x2713; |       | &#x2713; |         |
| [NodeStats](api/monitor.md#nodestats) | &#x2713; |       | &#x2713; |         |













