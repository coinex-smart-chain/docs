# CRC20 Token Standard

'CoinEx Smart Chain (CSC)' is fully compatible with Ethereum [ERC20](https://eips.ethereum.org/EIPS/eip-20) Standard.

```
// ----------------------------------------------------------------------------
// CRC Token Standard #20 Interface
// ----------------------------------------------------------------------------
contract CRC20Interface {
    function totalSupply() public constant returns (uint);
    function balanceOf(address tokenOwner) public constant returns (uint balance);
    function allowance(address tokenOwner, address spender) public constant returns (uint remaining);
    function transfer(address to, uint tokens) public returns (bool success);
    function approve(address spender, uint tokens) public returns (bool success);
    function transferFrom(address from, address to, uint tokens) public returns (bool success);

    // Optional
    function name() public view returns (string);
    function symbol() public view returns (string);
    function decimals() public view returns (uint8);

    event Transfer(address indexed from, address indexed to, uint tokens);
    event Approval(address indexed tokenOwner, address indexed spender, uint tokens);
}
```

* For standard, refer to [ERC20](https://eips.ethereum.org/EIPS/eip-20)
* For implementation, refer to [OpenZeppelin-ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC20)

## CRC20 Operation

### CRC20 ABI

```
ABI = '[{"constant":true,"inputs":[],"name":"name","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function","stateMutability":"view"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_value","type":"uint256"}],"name":"approve","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function","stateMutability":"nonpayable"},{"constant":true,"inputs":[],"name":"totalSupply","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function","stateMutability":"view"},{"constant":false,"inputs":[{"name":"_from","type":"address"},{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transferFrom","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function","stateMutability":"nonpayable"},{"constant":true,"inputs":[],"name":"decimals","outputs":[{"name":"","type":"uint8"}],"payable":false,"type":"function","stateMutability":"view"},{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function","stateMutability":"view"},{"constant":true,"inputs":[],"name":"symbol","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function","stateMutability":"view"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transfer","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function","stateMutability":"nonpayable"},{"constant":true,"inputs":[{"name":"_owner","type":"address"},{"name":"_spender","type":"address"}],"name":"allowance","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function","stateMutability":"view"},{"inputs":[{"name":"_totalSupply","type":"uint256"}],"payable":false,"type":"constructor","stateMutability":"nonpayable"},{"anonymous":false,"inputs":[{"indexed":true,"name":"from","type":"address"},{"indexed":true,"name":"to","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Transfer","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"owner","type":"address"},{"indexed":true,"name":"spender","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Approval","type":"event"}]'
```

### Connect CSC public nodes

#### JavaScript

* Mainnet

```JavaScript
const Web3 = require('web3');
// mainnet
const w3 = new Web3("https://rpc.coinex.net");
```

* Testnet

```JavaScript
const Web3 = require('web3');
const w3 = new Web3("https://testnet-rpc.coinex.net");
```

#### Python3

* Mainnet

```Python
from web3 import Web3
provider = Web3.HTTPProvider("https://csc-rpc.coinex.net")
w3 = Web3(provider)
```

* Testnet

```Python
from web3 import Web3
provider = Web3.HTTPProvider("https://testnet-rpc.coinex.net")
w3 = Web3(provider)
```

### CRC20 Inquiry

#### javascript

```javascript
const crc20_abi = "<crc20 contract abi>"
const contranctAddress = "<crc20 token address>";
const crcContract = new web3.eth.Contract(crc20_abi, contranctAddress);

// get total supply of crc20 token
crcContract.methods.totalSupply().call();

// get name of crc20 token
const name = crcContract.methods.name().call();

// get symbol of crc20 token
const symbol = crcContract.methods.symbol().call()

// get decimals of crc20 token
const decimals = crcContract.methods.decimals().call()

// get balance of address
const userAddress = '' // a user address
const balance = crcContract.methods.balanceOf(userAddress).call()
```

#### Python3

```python
# base crc20 info

# some crc20 token
crc20_address = "" 
crc20_address = Web3.toChecksumAddress(crc20_address)

# construct a crc20 contract object
contract = w3.eth.contract(crc20_address, abi=ABI)

# get total supply of crc20 token
total_supply = contract.functions.totalSupply().call()

# get name of crc20 token
name = contract.functions.name().call()

# get symbol of crc20 token
symbol = contract.functions.symbol().call()

# get decimals of crc20 token
decimals = contract.functions.decimals().call()

# get balance of address
address = '' # a user address
balance = contract.functions.balanceOf(address).call()

```

### CRC20 Transaction

#### javascript

```javascript
// crc20 transfer
const amount = '1000000000000000000' // Gwei
const toAddress = '0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe'; // target address
const data = crcContract.methods.transfer(toAddress, amount).encodeABI();
web3.eth.sendTransaction({
  from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe',
  to: contranctAddress, // crc20 constract
  data
}, function(error, hash){
// handler here
});
```

#### python3

```Python
crc20_address = Web3.toChecksumAddress(crc20_address)
contract = w3.eth.contract(crc20_address, abi=ABI)

# send amount
amount = 1 

# unlock a account
account_keyfile = "./keystore/XXXXXXXXXXXXXX"
password = "XXXXXXX"
w3 = get_web3_instance()
keyfile_json = eth_keyfile.load_keyfile(account_keyfile)
private_key_bytes = eth_keyfile.decode_keyfile_json(keyfile_json, password.encode('utf-8'))
account = w3.eth.account.privateKeyToAccount(private_key_bytes)

# get nonce of account
nonce = w3.eth.getTransactionCount(account.address)

# estimate gas
tx_obj = {'from': account.address, 'nonce': nonce}
gas = contract.functions.transfer(receiver, amount).estimateGas(tx_obj)

# get gas price
gas_price = w3.eth.gasPrice

tx_obj['gas'] = gas
tx_obj['gasPrice'] = gas_price

# construct the crc20 transfer transaction and sign
transaction = contract.functions.transfer(receiver, amount).buildTransaction(tx_obj)
signed = account.signTransaction(transaction)

# broadcast the signed transaction
tx_hash = w3.eth.sendRawTransaction(signed.rawTransaction)
tx_receipt = w3.eth.waitForTransactionReceipt(tx_hash)
```