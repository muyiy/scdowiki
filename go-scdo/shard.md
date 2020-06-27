# Address

**Shard** in SCDO is a characteristic and a collection of chain and addresses. Each address or chain belongs to a shard: SCDO mainnet contains 4 such shards. Each shard contains one shard and numerous addresses. To mine on the shard-1 chain, the miner address, or "coinbase", must be a shard-1 address. 

A privatekey matches one address for each shard. For example: 

```
Formats:
    private : "0x" + 64 hex characters
    address : shard + "S" + 40 hex characters

The privatekey:

0x14caa6d007e00bdbb5fd3db874b0b19f844da6892eeb5ed7027333d2a75fe608

matches the following addresses in each shard:

1Sa371c1ae41519e509c460959f52bb1266b1ad1d1
2Sa371c1ae41519e509c460959f52bb1266b1ad1d1
3Sa371c1ae41519e509c460959f52bb1266b1ad1d1
4Sa371c1ae41519e509c460959f52bb1266b1ad1d1
```

# Transaction

Two types of transaction exists on SCDO: **same-shard transaction** or **cross-shard transaction**. Same-shard means the transaction's receiver and sender are in the same shard, and cross shard means they're in different shards. The miner's address must be of the same shard as that of the chain, as mentioned, because miner reward is delivered in the form of a same-shard transaction from the shard's void address to the miner. 

SCDO's block time average around 14 seconds, which could be the maximal wait time for a same-shard transaction to be blocked, if internet connection and transaction traffic allows. For safer measures, it is recommended that the user wait for a few more blocks to be mined after the transaction is blocked, or "say let the transaction be blocked deeper", or "be blocked to a certain depth." The specific depth depends on the difficulty of the network: generally, the higher the difficulty, the less likely a softfork, and the smaller the depth needed.

A cross-shard transaction is done in two steps. First, a transaction on the sender's shard's chain, or "sender's chain", where the transaction amount is deducted from the sender's balance. Second, after the transaction reaches a depth of 120 on the sender's chain, a **debt** transaction is broadcasted to the receiver's chain, where the amount is added to the receiver's balance once the debt is blocked. And like recommended before, this 120 depth wait is for safety measures of cross shard transaction, specifically against double spending. A cross-shard transaction wait time would therefore translate to (14+120*14+14=) 1708s or 28 minutes.

# Contract

SCDO runs solidity engine: deploying or calling contract methods are done through transactions as well, though none-writing methods can be called through direct api requests. In short, __all transactions involving a contract must be same-shard__. 

A contract is deployed by sending a transaction to the void address, `1S0000000000000000000000000000000000000000`, with the hex format contract binary as the transaction payload. Once the transaction is blocked, a contract address of the same shard as the sender is generated. Transactions for calling a contract's write methods, or "call transactions", must be sent from address of the same shard as the contract.