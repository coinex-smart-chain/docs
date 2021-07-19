# FAQ

## Can validator's address, staker's address and reward receipt address be different?

`CSC` separates validator's address, staker's address and reward receipt address, they can be different。
Because the block needs to be signed, the `keystore` and password to the validator's address must be placed on the server.
Any address can stake to a validator. After the staker's address unstake and withdraw his staking, the staked `CET` will be returned to the original staker's address.
The reward of the validator will be uniformly allocated to the reward receipt address set by the validator, and only the reward receipt address can withdraw the reward.

> We suggest that the node builder separates validator's address and staker's address, so that the `keystore` and password of the staker do not need to be stored on the server, and there is no need to worry about the loss of the staker after the server is hacked.

## Can a staker's address be the CET address in the Coinex exchange?

No. Validator's address, staker's address and reward receipt address can't be the address in the Coinex exchange. You need to transfer your CET to an address on the `CSC` where you have the secret key.

## How to stake？

To make it easier for users to stake, `ViaWallet` is developing related features. In addition, the user can stake via command line operations, refer to [command-line operations](/validator_cli.md).

`cetd` needs `keystore` file to send transactions, In addition to creating a new address, you can also export the private key of a created address from `ViaWallet` to create `keystore` file.

First, export the private key from `ViaWallet` and save it to a file.
![ViaWallet export private key](./images/viawallet_export_privkey.png)

Then import the private key from the command line:
```
$ cetd account import YOUR-PRIVATE-KEY-FILE --datadir YOUR-KEYSTORE-PATH

INFO [07-03|00:03:06.072] Maximum peer count                       ETH=200 LES=0 total=200
INFO [07-03|00:03:06.080] Set global gas cap                       cap=25000000
Your new account is locked with a password. Please give a password. Do not forget this password.
Password:               # input keystore password
Repeat password:        # input keystore password again
```
- `YOUR-PRIVATE-KEY-FILE` fill in the private key file
- `YOUR-KEYSTORE-PATH` fill in the directory in which to save the `keystore` file
- When you meet error like `Fatal: Failed to load the private key: invalid character '2' at end of key file`, delete '0x' at the beginning of the private key
- The generated `keystore` file will be in `YOUR-KEYSTORE-PATH/keystore` with the file name like `UTC--2021-07-02T16-03-11.895849700Z--YOUR-ADDRESS`

## Can the validator node use the fast mode?

Yes.

## How to check node synchronization status?

You can check the height of your node with the `curl` command.
`curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":52}' -H "Content-Type: application/json" "http://127.0.0.1:8545"`

Or via `attach` command and go to the command line console
```
$ cetd attach data/cetd.ipc 
Welcome to the Geth JavaScript console!

instance: cetd/v1.0.0-stable-dfe1768e/linux-amd64/go1.15.6
at block: 455139 (Wed Jul 14 2021 15:06:32 GMT+0800 (CST))
 datadir: /root/workspace/csc-run-fullnode/data
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 senatus:1.0 txpool:1.0 web3:1.0

To exit, press ctrl-d
> eth.blockNumber
455141
```

## How long can the staking be withdrew after stake? How long can the staking be withdrew after unstake?

You can unstake at any time after you stake, but you need to wait for 86,400 blocks to withdraw your staking. Based on the current 3s block time, it probably needs to wait for 3 days.
Each time you unstake, you can only unstake and withdraw all the staking you have staked to the validator.

## How often can I withdraw the reward?

It must be more than 28,800 blocks since you withdrawn reward last time.

## How do you unjail a node?

If a node had been jailed, the first thing to do is investigate the cause. Restart the node after you fix the problem, and unjail the node through command line operation after the node is up and running properly and has been synchronized to the latest height.

## gasprice

`CSC` limits the transaction minimum gasprice to 500GWEI.
