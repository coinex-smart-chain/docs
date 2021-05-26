# 钱包账户管理

`web3`封装了一些和链交互的接口，方便我们进行`DApp`开发。我们可以通过`web3`封装的接口，使用不同的语言同`CSC`进行交互。
本文讲述如何通过`Web3`使用`javascript`, `python`在`CSC`上进行账户管理。

## 创建`web3`实例

### javascript

`javascript`主要使用库[`web3.js`](https://web3js.readthedocs.io/en/v1.3.4/)同`CSC`交互。

* 连接主网

```
const w3 = new Web3("https://rpc.coinex.net");
```

* 连接测试网

```
const w3 = new Web3("https://testnet-rpc.coinex.net");
```

### python3
`python`主要使用包[`Web3.py`](https://web3py.readthedocs.io/en/stable/)同`CSC`交互。

* 连接主网

```
from web3 import Web3
from web3.middleware import geth_poa_middleware
provider = Web3.HTTPProvider("https://rpc.coinex.net")
w3 = Web3(provider)
w3.middleware_onion.inject(geth_poa_middleware, layer=0)
```

* 连接测试网

```
from web3 import Web3
from web3.middleware import geth_poa_middleware
provider = Web3.HTTPProvider("https://testnet-rpc.coinex.net")
w3 = Web3(provider)
w3.middleware_onion.inject(geth_poa_middleware, layer=0)
```

## 创建账号

实例化`web3`之后，通过以下调用，可以随机返回一个账户：

### javascript

```
const account = w3.eth.accounts.create();
// print account
console.log(account);
/*
example:
{
  address: '0x00DE048c92eF8D6FeC6275E1907E38798808005d',
  privateKey: '0xc2a58a08abcd566348a6d2798b0b074fc8b7b66a650a7aaf463e6d36b4b9776e',
  signTransaction: [Function: signTransaction],
  sign: [Function: sign],
  encrypt: [Function: encrypt]
}
*/
```

### python

```
account = w3.eth.account.create();
# print private key
print(account.privateKey.hex())
# example: `0x9b308e83c8120818a721fc999618d8869da61c0b440386b963523bcb26fe9839'

# print address
print(account.address)
# example: '0xC286d47ABE4C9B8B2F724610B9eb9e91D7a7De9A'
```

## 通过秘钥恢复账号

如果你有私钥，你也可以直接通过`web3`进行恢复你在`csc`上的账号。

### javascript

```
const account = w3.eth.accounts.privateKeyToAccount("your private key string")
```

### python3

```
account = w3.eth.account.privateKeyToAccount("your private key string")
```
