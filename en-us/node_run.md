# Run

## Hardware requirements

### Mainnet
* Recommended

```
CPU: 16Core
RAM: 32GB
HDD: SSD 1TB
```

* Minimum

```
CPU: 8Core
RAM: 16GB
HDD: SSD 500GB
```

### Testnet

```
CPU: 8Core
RAM: 16GB
HDD: SSD 500GB
```

### Network

* Public network IP 
* Open TCP/UDP port for P2P discovery and interconnection. Default P2P portal.
  * Mainnet: `36652`
  * Testnet: `36653`

## Run

### Prepare

Firstly, starting `CSC` requires the 'cetd' binary file:
* Download code from [github](https://github.com/coinex-smart-chain/csc), [compile](/en-us/node_compile.md) and get cetd.
* Directly download [Binary package cetd](https://github.com/coinex-smart-chain/csc).

### Initialize

Initialize command:
```
cetd --datadir /path/your-data-localtion-fold init
```

This command will create the data directory and `keystore` directory under `/path/your-data-localtion-fold`, and create Genesis Block. If the default `--datadir` is not specified, it will create `.cetd` as the data directory and 'keystore' directory in the current user's `home` directory. As follows:

```
/root/.cetd
├── cetd
│   ├── chaindata
│   │   ├── 000001.log
│   │   ├── CURRENT
│   │   ├── LOCK
│   │   ├── LOG
│   │   └── MANIFEST-000000
│   ├── lightchaindata
│   │   ├── 000001.log
│   │   ├── CURRENT
│   │   ├── LOCK
│   │   ├── LOG
│   │   └── MANIFEST-000000
│   ├── LOCK
│   └── nodekey
└── keystore
```

By default, `init` command is initialized to Mainnet information, and `--testnet` option is initialized to testnet information.

### Run

Startup command:
```
cetd --datadir /path/your-data-localtion-fold
```
By default, the synchronization mode is `fast`, which can be changed to `full` mode with the option `--syncmode full`.
We have assigned P2P seed Node in `cetd` by default. You can change and assign trusted Seed Nodes via `--bootnodes` options.

### Configuration

To make it easy for all users to deploy `CSC` nodes, we have integrated some default configuration into the binary package 'cetd' file so that everyone can start without any configuration. For professional users, you can refer to the following configuration, optimize the configuration, and then start the command as: `cetd --config ./<your config file>`

```
[Eth]
NetworkId = 53
SyncMode = "fast"
NoPruning = false
NoPrefetch = false
LightPeers = 100
UltraLightFraction = 75
DatabaseCache = 512
DatabaseFreezer = ""
TrieCleanCache = 256
TrieDirtyCache = 256
TrieTimeout = 100000000000
EnablePreimageRecording = false
EWASMInterpreter = ""
EVMInterpreter = ""

[Eth.Miner]
GasFloor = 30000000
GasCeil = 42000000
GasPrice = 100000000000
Recommit = 10000000000
Noverify = false

[Eth.TxPool]
Locals = []
NoLocals = true
Journal = "transactions.rlp"
Rejournal = 3600000000000
PriceLimit = 100000000000
PriceBump = 10
AccountSlots = 16
GlobalSlots = 4096
AccountQueue = 64
GlobalQueue = 1024
Lifetime = 10800000000000

[Eth.GPO]
Blocks = 20
Percentile = 60

[Node]
IPCPath = "cetd.ipc"
HTTPHost = "0.0.0.0"
NoUSB = true
InsecureUnlockAllowed = false
HTTPPort = 8545
HTTPVirtualHosts = ["localhost"]
HTTPModules = ["eth", "net", "web3", "txpool", "senatus"]
WSPort = 8546
WSModules = ["net", "web3", "eth"]

[Node.P2P]
MaxPeers = 200
NoDiscovery = false
StaticNodes = ["enode://6d97c62365495e706739822bf231bc4b13ad66ca0a5664965d437e40087c6c76f2cedf1286fffbcec2fc1500aa2634c70a26b2c7408c85081578ab85069b919f@47.242.178.212:36653", "enode://b858216d3c626dcc83ce6c9169d243cd8ebadd0dcdb67cdba5d63c4b6d6989c0a8fdf2278d5b68e20cc8eeefa8eb58cf4d5bb0c3dda3cbfae3e42586eb6897bb@47.242.181.109:36653"]
TrustedNodes = []
ListenAddr = ":36653"
EnableMsgEvents = false

[Node.HTTPTimeouts]
ReadTimeout = 30000000000
WriteTimeout = 30000000000
IdleTimeout = 120000000000
```