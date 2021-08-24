# 启动节点

## 硬件配置要求

### 主网
* 推荐配置

```
cpu: 16core
内存: 32g
硬盘: ssd 1T
```

* 最低要求

```
cpu: 8core
内存: 16g
硬盘: ssd 500GB
```

### 测试网

```
cpu: 8core
内存: 16g
硬盘: ssd 500GB
```

### 网路

* 公网IP
* 开放TCP/UDP端口，便于p2p发现和互联， 默认p2p端口
  * 主网：`36652`
  * 测试网：`36653`

## 运行

### 准备

启动`CSC`首先需要`cetd`二进制文件：
* 可以从[github](https://github.com/coinex-smart-chain/csc)下载源代码[编译](./node_compile.md)得到`cetd`
* 直接下载[二进制包cetd](https://github.com/coinex-smart-chain/csc/releases)

### 初始化节点

初始化命令：
```
cetd --datadir /path/your-data-localtion-fold init
```

该命令将在目录`/path/your-data-localtion-fold`创建数据目录及`keystore`目录，
并创建创世区块。如果不指定默认`--datadir`会在当前用户的`home`目录下创建名为`.cetd`作为
数据目录及`keystore`目录，如下：

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

默认情况下，`init`命令初始化为主网信息，通过`--testnet`选项初始化为测试网信息。

### 启动

启动命令：

```
cetd --datadir /path/your-data-localtion-fold
```

默认情况下，启动连接的是`CSC`主网，并且同步方式为`full`。我们可以通过通过指定`--testnet`选项启动测试网，通过选项`--syncmode fast`修改为快速同步方式。我们在`cetd`已经默认指定了p2p seed节点，如果想指定其他信任的seed节点，可以通过`--bootnodes`选项指定。

### 节点配置

为使大家能够很容易的部署`CSC`节点，我们将一些默认配置集成到二进制包`cetd`文件中，任何人无需任何配置即可启动。对于专业用户，可以参考以下配置，进行优化配置，然后启动命令为：`cetd --config ./<your config file>`

例如：测试网config

```
[Eth]
NetworkId = 53
SyncMode = "full"
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
GasPrice = 500000000000
Recommit = 10000000000
Noverify = false

[Eth.TxPool]
Locals = []
NoLocals = true
Journal = "transactions.rlp"
Rejournal = 3600000000000
PriceLimit = 500000000000
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