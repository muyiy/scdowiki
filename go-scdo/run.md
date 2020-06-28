# Keyfile

Configuring miner node requires two basic things: a p2p id, and a miner address. It is highly recommended that the miner's privatekey is protected.

There are many ways to save a privatekey: printing, writing, mnemonic words, hd wallets, and etc. Keyfile being one of the most convenient one is available via a `client` command: `savekey`. The [shard tutorial](shard.md) mentioned how to generate a pair of keys by shard. Every command works with the `-h` help option. 

```
$ ./client savekey -h

NAME:
   client savekey - save private key to a keystore file

USAGE:
   client savekey [command options] [arguments...]

OPTIONS:
   --privatekey value  private key for account
   --file value        key store file name
```
Example:
```
$ ./client key --shard 1
public key:  1Sfe11f81e3da032dd3d0728795d90620ec161ecf1
private key: 0x8b73d1aecaba56557d4f235fe99df3b2b689bb3346b87892fc631d57cabef75f 

$ ./client savekey --file mykey --privatekey 0x8b73d1aecaba56557d4f235fe99df3b2b689bb3346b87892fc631d57cabef75f 
Password: 
Repeat password:
store key successfully, the key file path is mykey
```

Recovering privatekey with keyfile and password: 
```
$ ./client deckeyfile --file mykey
Please input your key file password: 
public key:  1Sfe11f81e3da032dd3d0728795d90620ec161ecf1
private key: 0x8b73d1aecaba56557d4f235fe99df3b2b689bb3346b87892fc631d57cabef75f
```

# Configure

The configuration file is in json format. There are templates that comes with the binaries from [go-scdo releases](https://github.com/scdoproject/go-scdo/releases). It is also in `go-scdo/cmd/node/config` of `go-scdo`'s source code. `node1.json` is for shard 1, `node2.json` is for shard 2 and etc. 

Replace the `basic.coinbase` field's default address with your miner address. Then use the `./client key` to generate another privatekey (shard doesn't matter) to replace `p2p.privateKey` field's default value with your newly generated privatekey. The former makes the mining rewards goes to your address, and the latter is necessary for p2p connection. <u>All necessary changes are done at this point.</u>

All the addresses in the templates are configurable. `basic.address` is for client queries. `p2p.address` is for exposing self node, and `p2p.staticNodes` is for discovering other nodes. `httpServer.address` is for http requests, which is also where `scdo.js`' rpc module query from.

For developers, leave `p2p.staticNodes` as an empty array, `[]` to run individually. Toggle `log.printLog` to silence log printout when testing specific functions with non-log printouts. Difficulty is adjustable in `genesis.difficult`.

# Run

The `--config` option needs the absolute path or path relative to the `node` binary to your config file.

```
# basic mining 
$ ./node start -c node1.json

# multiple threads
$ ./node start -c node1.json --threads 8

# synchronize only, don't mine
$ ./node start -c node1.json -m stop

# recover from lower hights if corrupted 
$ ./node start -c node1.json --startheight 1000
```

Start another terminal then monitor your node server by the `./client getinfo` command. The value fed to the `-a` option address port should match the value in `basic.address` of the config file.

```
$ ./client getinfo -a localhost:8027

{
	"BlockAge": 28,
	"Coinbase": "1S7801a0ff61cae77f0bf43065c25a1f9c6b62fff1",
	"CurrentBlockHeight": 2977914,
	"HeaderHash": "0x136d766a03c373a35488bbcbeb6ea419cc5af25374ef97726b9031ea9329a819",
	"MinerStatus": "Stopped",
	"PeerCnt": "13 (4 4 2 3)",
	"Shard": 1,
	"Version": "SCDO_v1.0.0"
}
```

For more ways to use `node` services through `client`, refer to the [api tutorial](api.md). 

# Appendix 

The keyfile format:
```
$ cat mykey
{
	"version": 1,
	"address": "1Sfe11f81e3da032dd3d0728795d90620ec161ecf1",
	"crypto": {
		"ciphertext": "8519aa2d6cb433457d255053cce6e91518c7baeecd47ec2b66e5fe6c6cc11944",
		"iv": "1eeae34283e24f6122c0c9abf25f3a01",
		"salt": "17b109af59a8a7882c01921ef6d0d19b26fdbc6b04025e398d7575bc72c05a5a",
		"mac": "0x71fa8df5d584472bf54aae09e3a6445229a364f932c5edb955619cc761166f8c"
	}
}
```

The configuration format:

```
{
    "basic": {
        "name": "scdo node1",
        "version": "1.0",
        "dataDir": "node1",
        "address": "0.0.0.0:8027",
        "coinbase": "1Scee66ad4a1909f6b5170dec230c1a69bfc2b21d1",
        "algorithm": "mpow"
    },
    "p2p": {
        "privateKey": "0xf65e40c6809643b25ce4df33153da2f3338876f181f83d2281c6ac4a987b1479",
        "staticNodes": [
            "198.251.69.156:8057"
        ],
        "address": "0.0.0.0:8057",
        "networkID": "scdo"
    },
    "log": {
        "isDebug": false,
        "printLog": true
    },
    "httpServer": {
        "address": "0.0.0.0:8037",
        "crossorigins": [
            "*"
        ],
        "whiteHost": [
            "*"
        ]
    },
    "wsserver": {
        "address": "0.0.0.0:8047",
        "crossorigins": [
            "*"
        ]
    },
    "ipcconfig": {
        "name": "scdo1.ipc"
    },
    "metrics": {
        "address": "0.0.0.0:8087",
        "duration": 10,
        "database": "influxdb",
        "username": "test",
        "password": "test123"
    },
    "genesis": {
        "difficult": 5200000,
        "shard": 1,
        "timestamp": 1554099618
    }
}
```