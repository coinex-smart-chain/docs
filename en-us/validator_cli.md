## Node CLI
Using `cetd --help` to check instructions of each operation and supported parameter options, and then introduce operations related to validator node.

Parameter options related to validator node:

| Option | Descripition |
| --- | ----------- |
|`--from`| The address who create the transaction|
|`--validator.address`| Validator's address|
|`--validator.rewardaddr` | Validator's reward receipt address|
|`--validator.moniker` | Validator's nickname|
|`--validator.website` | Validator's website|
|`--validator.email` | Validator's email|
|`--validator.detail` | Validator's description|
|`--validator.staking` | Staking amount(the unit is Wei, 1CET = 10^18Wei)|
|`--validator.staker` | Staker's address|
|`--node`| Node RPC to connect to|
|`--nonce`| Nonce of this address|
|`--tx.gaslimit` | Gas limit of this transaction|
|`--tx.gasprice` | Gas price of this transaction|
|`--keystore` | Key file path of this address|
|`--password` | Key file password of this address| 

### Create validator node

`cetd validator.create --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec  --validator.rewardaddr 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.moniker '<your node moniker>' --validator.website '<your home site>' --validator.email '<your contract email>' --validator.detail '<your node description>' --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### Edit validator node

`cetd validator.edit --from 0x42eacf5b37540920914589a6b1b5e45d82d0c1ca --validator.rewardaddr 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.moniker '<your node moniker>' --validator.website '<your home site>' --validator.email '<your contract email>' --validator.detail '<your node description>' --keystore ./data/keystore/  --node http://127.0.0.1:8545`

### Stake for validator node

`cetd staking --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.address 0x42eacf5b37540920914589a6b1b5e45d82d0c1ca --validator.staking 10000000000000000000000 --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### Unstake

`cetd unstaking --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.address 0x42eacf5b37540920914589a6b1b5e45d82d0c1ca --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### Withdraw staking

`cetd withdrawstake --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### Withdraw reward

`cetd withdrawreward --from 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.address 0x42eacf5b37540920914589a6b1b5e45d82d0c1ca --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### Unjail node

`cetd unjail --from 0x582bd2e02494dc6beb9a14401f4eae009533484c --keystore ./data/keystore/ --node http://127.0.0.1:8545`

### Inquire validator description info

`cetd validator.description.query --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --node http://127.0.0.1:8545`

### Inquire node info such as block generation, reward, etc

`cetd validator.info.query --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --node http://127.0.0.1:8545`

### Inquire activated node list

`cetd validator.activated.query --node http://127.0.0.1:8545`

### Inquire candidate node list

`cetd validator.candidators.query --node http://127.0.0.1:8545`

### Inquire staking info from any address to node

`cetd validator.staking.query --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --validator.staker 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --node http://127.0.0.1:8545`

### Inquire validator penalty record

`cetd validator.slash.record --validator.address 0x65804ab640b1d4db5733a36f9f4fd2877e4714ec --node http://127.0.0.1:8545`
