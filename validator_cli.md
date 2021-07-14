## 节点CLI
通过`cetd --help`查看各个操作命令说明，及支持的参数选项。接下来介绍验证节点相关的操作。

验证节点相关的参数选项：

| 选项 | 描述 |
| --- | ----------- |
|`--from`| 交易创建地址 |
|`--validator.address`| 验证节点地址|
|`--validator.rewardaddr` | 验证节点收益接收地址|
|`--validator.moniker` | 验证节点昵称|
|`--validator.website` | 验证节点官网|
|`--validator.email` | 验证节点邮箱|
|`--validator.detail` | 验证节点描述|
|`--validator.staking` | 质押数量（单位为Wei，1CET = 10^18Wei）|
|`--validator.staker` | 质押者地址|
|`--node`| 连接节点rpc|
|`--nonce`| 指定交易地址nonce|
|`--tx.gaslimit` | 指定交易gas limt|
|`--tx.gasprice` | 指定交易gas price|
|`--keystore` | 指定地址所在路径|
|`--password` | 指定地址key file的密码|

### 创建验证节点

`cetd validator.create --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec  --validator.rewardaddr 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.moniker '<your node moniker>' --validator.website '<your home site>' --validator.email '<your contract email>' --validator.detail '<your node description>' --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### 编辑验证节点

`cetd validator.edit --from 0x42eacf5b37540920914589a6b1b5e45d82d0c1ca --validator.rewardaddr 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.moniker '<your node moniker>' --validator.website '<your home site>' --validator.email '<your contract email>' --validator.detail '<your node description>' --keystore ./data/keystore/  --node http://127.0.0.1:8545`

### 给验证节点质押

`cetd staking --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec  --validator.address 0x42eacf5b37540920914589a6b1b5e45d82d0c1ca --validator.staking 10000000000000000000000 --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### 解除质押

`cetd unstaking --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.address 0x42eacf5b37540920914589a6b1b5e45d82d0c1ca --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### 提取质押

`cetd withdrawstake --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### 提取出块奖励

`cetd withdrawreward --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.address 0x42eacf5b37540920914589a6b1b5e45d82d0c1ca --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### 释放出块节点

`cetd unjail --from 0x582bd2e02494dc6beb9a14401f4eae009533484c --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### 查询节点的描述信息

`cetd validator.description.query --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --node http://127.0.0.1:8545`

### 查询节点的出块及奖励等信息

`cetd validator.info.query --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --node http://127.0.0.1:8545`

### 获取当前出块节点列表

`cetd validator.activated.query --node http://127.0.0.1:8545`

### 获取出块节点候选列表

`cetd validator.candidators.query --node http://127.0.0.1:8545`

### 获取某个地址对某个出块节点的质押信息

`cetd validator.staking.query --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.staker 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --node http://127.0.0.1:8545`

### 查看出块节点错失的区块数

`cetd validator.slash.record --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --node http://127.0.0.1:8545`
