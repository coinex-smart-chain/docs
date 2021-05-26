# Wallet account management

Some interfaces that interact with the chain have been encapsulated by `web3` to facilitate our `DApp` development. Via theses `web3` encapsulated interfaces, we can use different languages to interact with `CSC`. 
This article elaborates on how to use `JavaScript` and `Python` to manage accounts on `CSC` through `Web3`.

## Create instances of `web3`

### javascript

Mostly, `javascript` uses database[`web3.js`](https://web3js.readthedocs.io/en/v1.3.4/) to interact with `CSC`.

* Connect to Mainnet

```
const w3 = new Web3("https://rpc.coinex.net");
```

* Connect to Testnet

```
const w3 = new Web3("https://testnet-rpc.coinex.net");
```

### python3
Mostly, `python` uses package[`Web3.py`](https://web3py.readthedocs.io/en/stable/)to interact with `CSC`.

* Connect to Mainnet

```
from web3 import Web3
from web3.middleware import geth_poa_middleware
provider = Web3.HTTPProvider("https://rpc.coinex.net")
w3 = Web3(provider)
w3.middleware_onion.inject(geth_poa_middleware, layer=0)
```

* Connect to Testnet

```
from web3 import Web3
from web3.middleware import geth_poa_middleware
provider = Web3.HTTPProvider("https://testnet-rpc.coinex.net")
w3 = Web3(provider)
w3.middleware_onion.inject(geth_poa_middleware, layer=0)
```

## Create an account

After instantiating `web3`, you can return a random account with the following call:

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

## Recover account via private key

You can also recover your account on `CSC` directly through `web3` if you have access to your private key.

### javascript

```
const account = w3.eth.accounts.privateKeyToAccount("your private key string")
```

### python3

```
account = w3.eth.account.privateKeyToAccount("your private key string")
```
