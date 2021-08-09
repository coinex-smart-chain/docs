# NFT

`NFT` means non-fungible token, that is, each token is unique.

And `ERC721` is a standard for representing ownership of [non-fungible tokens](https://docs.openzeppelin.com/contracts/3.x/tokens#different-kinds-of-tokens) in Ethereum.

`CSC` is fully compatible with Ethereum [ERC721](https://eips.ethereum.org/EIPS/eip-721) Standard.

```
// ----------------------------------------------------------------------------
// CRC Token Standard #721 Interface
// ----------------------------------------------------------------------------
contract CRC721Interface {
    function balanceOf(address _owner) external view returns (uint256);
    function ownerOf(uint256 _tokenId) external view returns (address);
    function safeTransferFrom(address _from, address _to, uint256 _tokenId, bytes data) external payable;
    function safeTransferFrom(address _from, address _to, uint256 _tokenId) external payable;
    function transferFrom(address _from, address _to, uint256 _tokenId) external payable;
    function approve(address _approved, uint256 _tokenId) external payable;
    function setApprovalForAll(address _operator, bool _approved) external;
    function getApproved(uint256 _tokenId) external view returns (address);
    function isApprovedForAll(address _owner, address _operator) external view returns (bool);

    // ERC165
    function supportsInterface(bytes4 interfaceID) external view returns (bool);

    // Optional
    function name() external view returns (string _name);
    function symbol() external view returns (string _symbol);
    function tokenURI(uint256 _tokenId) external view returns (string);
    
    function totalSupply() external view returns (uint256);
    function tokenByIndex(uint256 _index) external view returns (uint256);
    function tokenOfOwnerByIndex(address _owner, uint256 _index) external view returns (uint256);

    // Event
    event Transfer(address indexed _from, address indexed _to, uint256 indexed _tokenId);
    event Approval(address indexed _owner, address indexed _approved, uint256 indexed _tokenId);
    event ApprovalForAll(address indexed _owner, address indexed _operator, bool _approved);
}
```

- For standard, refer to [ERC721](https://eips.ethereum.org/EIPS/eip-721)
- For implementation, refer to [OpenZeppelin-ERC721](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC721)

## CRC721 Operation

### CRC721 ABI

```
ABI = '[{"inputs":[{"internalType":"string","name":"name_","type":"string"},{"internalType":"string","name":"symbol_","type":"string"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"owner","type":"address"},{"indexed":true,"internalType":"address","name":"approved","type":"address"},{"indexed":true,"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"Approval","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"owner","type":"address"},{"indexed":true,"internalType":"address","name":"operator","type":"address"},{"indexed":false,"internalType":"bool","name":"approved","type":"bool"}],"name":"ApprovalForAll","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"from","type":"address"},{"indexed":true,"internalType":"address","name":"to","type":"address"},{"indexed":true,"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"Transfer","type":"event"},{"inputs":[{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"approve","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"owner","type":"address"}],"name":"balanceOf","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"burn","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"exists","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"getApproved","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"owner","type":"address"},{"internalType":"address","name":"operator","type":"address"}],"name":"isApprovedForAll","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"name","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"ownerOf","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"},{"internalType":"bytes","name":"_data","type":"bytes"}],"name":"safeMint","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"safeMint","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"from","type":"address"},{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"safeTransferFrom","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"from","type":"address"},{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"},{"internalType":"bytes","name":"_data","type":"bytes"}],"name":"safeTransferFrom","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"operator","type":"address"},{"internalType":"bool","name":"approved","type":"bool"}],"name":"setApprovalForAll","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"bytes4","name":"interfaceId","type":"bytes4"}],"name":"supportsInterface","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"symbol","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"tokenURI","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"from","type":"address"},{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"transferFrom","outputs":[],"stateMutability":"nonpayable","type":"function"}]'
```

### Connect CSC public nodes

#### javascript

* Mainnet

```Javascript
const Web3 = require('web3');
const w3 = new Web3("https://rpc.coinex.net");
```

* Testnet

```Javascript
const Web3 = require('web3');
const w3 = new Web3("https://testnet-rpc.coinex.net");
```

#### python3

* Mainnet

```python
from web3 import Web3
provider = Web3.HTTPProvider("https://rpc.coinex.net")
w3 = Web3(provider)
```

* Testnet

```python
from web3 import Web3
provider = Web3.HTTPProvider("https://testnet-rpc.coinex.net")
w3 = Web3(provider)
```

### crc721 Inquiry

#### javascript

```javascript
const crc721_abi = "<crc721 contract abi>";
const contranctAddress = "<crc721 token address>";
const crcContract = new web3.eth.Contract(crc721_abi, contranctAddress);

// get name of crc721 token
const name = crcContract.methods.name().call();

// get balance of address
const userAddress = '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'; // a user address
const balance = crcContract.methods.balanceOf(userAddress).call();

// ...
```

#### python3

```python
crc721_address = "<crc721 token address>" 
crc721_address = Web3.toChecksumAddress(crc721_address)
crc721_abi = "<crc721 contract abi>"

# construct a crc721 contract object
contract = w3.eth.contract(crc721_address, abi=crc721_abi)

# get name of crc721 token
name = contract.functions.name().call()

# get balance of address
address = '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe' 	# a user address
balance = contract.functions.balanceOf(address).call()

# ...
```

### crc721 Transaction

#### javascript

```javascript
// crc721 safeTransferFrom

const fromAddress = '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe';
const toAddress = '0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe';
const tokenId = 1;

// construct the crc721 safeTransferFrom transaction
const data = crcContract.methods.safeTransferFrom(fromAddress, toAddress, tokenId).encodeABI();

web3.eth.sendTransaction({
  from: sender,						// transaction sender address
  to: contranctAddress, 	// crc721 contract address
  data
}, function(error, hash){
	// handler here
});

// ...
```

#### python3

```python
# crc721 safeTransferFrom

crc721_address = Web3.toChecksumAddress(crc721_address)
contract = w3.eth.contract(crc721_address, abi=crc721_abi)

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
gas = contract.functions.safeTransferFrom(fromAddress, toAddress, tokenId).estimateGas(tx_obj)

# get gas price
gas_price = w3.eth.gasPrice

tx_obj['gas'] = gas
tx_obj['gasPrice'] = gas_price

# construct the crc721 safeTransferFrom transaction and sign
transaction = contract.functions.safeTransferFrom(fromAddress, toAddress, tokenId).buildTransaction(tx_obj)
signed = account.signTransaction(transaction)

# broadcast the signed transaction
tx_hash = w3.eth.sendRawTransaction(signed.rawTransaction)
tx_receipt = w3.eth.waitForTransactionReceipt(tx_hash)

# ...
```

