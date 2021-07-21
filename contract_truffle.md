# Truffle

[truffle](https://www.trufflesuite.com/) 是帮助合约开发的强大工具。

## 环境安装

* node

参见 [Installing Node.js](https://nodejs.org/en/download/package-manager/)。

* truffle

安装 truffle

```shell
npm install -g truffle
```

安装完成后执行以下命令

```shell
truffle version
```

显示类似以下信息，则表示安装成功。

```
Truffle v5.3.3 (core: 5.3.3)
Solidity v0.5.16 (solc-js)
Node v14.16.1
Web3.js v1.3.5
```

## 创建项目

创建项目文件夹

```shell
mkdir mydapp
cd mydapp/
```

使用 truffle 初始化项目

```shell
truffle init
```

项目初始化后目录结构如下：

```
|-- contracts         //文件夹，用于放置合约文件
|-- migrations        //文件夹，用于放置部署脚本
|-- test              //文件夹，用于放置测试文件
|-- truffle-config.js //此项目的 truffle 配置文件
```

修改配置文件

```
const HDWalletProvider = require('@truffle/hdwallet-provider');
const fs = require('fs');
const mnemonic = fs.readFileSync(".secret").toString().trim();

module.exports = {

  networks: {
    testnet: {
      provider: () => new HDWalletProvider(mnemonic, 'https://testnet-rpc.coinex.net'),
      network_id: 53,
      gasPrice: 500000000000
    },
    mainnet: {
      provider: () => new HDWalletProvider(mnemonic, 'https://rpc.coinex.net'),
      network_id: 52,
      gasPrice: 500000000000
    }
  },

  // Set default mocha options here, use special reporters etc.
  mocha: {
    // timeout: 100000
  },

  // Configure your compilers
  compilers: {
    solc: {
      // version: "^0.6.12",
    }
  }
};
```

请注意，这里要求为Provider传递私钥，这是您部署合约使用的帐户私钥。在项目根目录中创建一个新的.secret文件，从Metamask钱包中获取私钥，写到.secret文件中。

## 编写合约

将自定义的合约放入 `contracts` 文件夹内，并修改 `migrations` 文件夹中的部署脚本。

## 部署合约

运行部署命令

```shell
truffle migrate --network testnet
```

我们以 MetaCoin 项目为例，合约代码如下：

```
pragma solidity >=0.4.25 <0.7.0;

import "./ConvertLib.sol";

// This is just a simple example of a coin-like contract.
// It is not standards compatible and cannot be expected to talk to other
// coin/token contracts. If you want to create a standards-compliant
// token, see: https://github.com/ConsenSys/Tokens. Cheers!

contract MetaCoin {
	mapping (address => uint) balances;

	event Transfer(address indexed _from, address indexed _to, uint256 _value);

	constructor() public {
		balances[tx.origin] = 10000;
	}

	function sendCoin(address receiver, uint amount) public returns(bool sufficient) {
		if (balances[msg.sender] < amount) return false;
		balances[msg.sender] -= amount;
		balances[receiver] += amount;
		emit Transfer(msg.sender, receiver, amount);
		return true;
	}

	function getBalanceInEth(address addr) public view returns(uint){
		return ConvertLib.convert(getBalance(addr),2);
	}

	function getBalance(address addr) public view returns(uint) {
		return balances[addr];
	}
}
```

输出结果如下：

```

Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.



Starting migrations...
======================
> Network name:    'testnet'
> Network id:      53
> Block gas limit: 6721975 (0x6691b7)


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0xc92b16882582cab42a92ed0272133cdb36291b02561b192fef609110549ca8ae
   > Blocks: 0            Seconds: 0
   > contract address:    0xF73901C6560B5fb487FAbF391C1Ce6b1E1B6B8F6
   > block number:        1
   > block timestamp:     1620896663
   > account:             0x3845970B03eDD143295Ae2B1EaE73Beb1ddFd6f3
   > balance:             99.9967165
   > gas used:            164175 (0x2814f)
   > gas price:           500 gwei
   > value sent:          0 ETH
   > total cost:          0.0032835 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:           0.0032835 ETH


2_deploy_contracts.js
=====================

   Deploying 'ConvertLib'
   ----------------------
   > transaction hash:    0xa94c9b9ecd732990ae7d2a69a20061f2ab6f23c6ac8caa1e0380204d32a831d3
   > Blocks: 0            Seconds: 0
   > contract address:    0x2f32569cD13C389D430384654092275DcD4691E3
   > block number:        3
   > block timestamp:     1620896664
   > account:             0x3845970B03eDD143295Ae2B1EaE73Beb1ddFd6f3
   > balance:             99.99396028
   > gas used:            95470 (0x174ee)
   > gas price:           500 gwei
   > value sent:          0 ETH
   > total cost:          0.0019094 ETH


   Linking
   -------
   * Contract: MetaCoin <--> Library: ConvertLib (at address: 0x2f32569cD13C389D430384654092275DcD4691E3)

   Deploying 'MetaCoin'
   --------------------
   > transaction hash:    0x8079e79c2055b1fcfcaee0f6c9147805b5d3c0046466f695a862e8692ec9ece2
   > Blocks: 0            Seconds: 0
   > contract address:    0xA271b814E956AcE4b5c8d68613B44C245dbfA9a8
   > block number:        4
   > block timestamp:     1620896664
   > account:             0x3845970B03eDD143295Ae2B1EaE73Beb1ddFd6f3
   > balance:             99.98822898
   > gas used:            286565 (0x45f65)
   > gas price:           500 gwei
   > value sent:          0 ETH
   > total cost:          0.0057313 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:           0.0076407 ETH


Summary
=======
> Total deployments:   3
> Final cost:          0.0109242 ETH
```

## 合约交互

进入交互控制台

```shell
truffle console --network testnet
truffle(testnet)> 
```

获取合约抽象

```
truffle(testnet)> let instance = await MetaCoin.deployed()
undefined
truffle(testnet)> instance
```

在控制台发起一笔交易

以调用合约`sendCoin`方法为例：

```
truffle(testnet)> let accounts = await web3.eth.getAccounts()
truffle(testnet)> instance.sendCoin(accounts[1], 10, {from: accounts[0]})
```

在控制台发起一次调用

以调用合约`getBalance`方法为例：

```
truffle(testnet)> let balance = await instance.getBalance(accounts[0])
truffle(testnet)> balance.toNumber()
```
