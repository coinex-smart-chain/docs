# About CSC Consensus

`CoinEx Smart Chain (CSC)` adopts `CPoS` consensus protocol and is fully compatible with `Ethereum virtual machine (EVM)` on support for high performance transactions, with a maximum capacity of up to 101 validators simultaneously. Meanwhile, `CSC` adheres to the principle of decentralization and permission-free so that anyone can become a validator by staking `CET`.

Goals of `CSC`:
1. Shorter time period for block generation 
2. Higher compatibility with Ethereum
3. Decentralization

## CPoS Consensus

Although `Proof of Work (PoW)` has been proved to be a practical solution for decentralized networks, yet it is not environment-friendly and requires a large number of participants to maintain network security.

On the other hand, Ethereum and some other networks use `Proof of Authority (PoA)` or its variants in different scenarios, including test network and main network. `PoA` provides defense for 51% attack and is more effective in preventing evil-doing by some Byzantine nodes. However, `PoA` protocol is not decentralized enough, for the validators are prone to corruption and security attacks given the extreme powers they possess. 

Therefore, some blockchain projects introduce other consensus schemes on the premise of ensuring network security and stability without compromising decentralization, such as `DPoS` adopted by EOS and Cosmos, which allows token holders to vote for validator nodes and makes the blockchain more decentralized and conducive to community management.

After rigorous investigation and research, CoinEx Team adheres to the principle of decentralization and combines the characteristics of `PoS` with `PoA` to realize `CPoS`, without losing network stability and security. The features of `CPoS` are as follows:

1. Blocks are generated with a maximum of 101 validator nodes.
2. Anyone can become a validator by staking `CET` without any permitted.
3. Validators take turns to generate blocks. When the validator node produce blocks normally, the difficulty is 2; when the validator node do not produce blocks in a predetermined order, the difficulty is reduced to 1; when the block forks, the chain with the greatest difficulty will be systematically selected.
4. Anyone can stake for their trusted validator.

## Basic concepts

1. Validator

Everyone is welcome to apply and become validator by staking `CET`. The first staking for the validator must exceed `10000 CET` and each subsequent staking must exceed `1000CET`. Based on overall staking ranking, the blockchain will select the top 101 nodes as validators in every 200 blocks. The validator has the obligation to generate blocks and verify on-chain info. In return, the validator will be rewarded with block commission fees and a certain amount of block production reward (currently `1 CET`) on the basis of the proportion of their staking.

2. Staking

Everyone is welcome to assist nodes to become validator by staking `CET`. The assets can be unstaked directly via contract calls or command operations and these `CET` will be available for withdrawal after 86,400 blocks.

3. System contract

`CSC` manages node staking and governance via system contracts. The system contract has been deployed after `CSC` launch. Currently, 2 sets of system contracts are designed for `CSC`:

* Validator contract

Via staking contract, anyone can create nodes, stake for the nodes and make profits.

* Slash contract

Due to network, hardware, configuration and other factors, `CSC` might suffer from instability led by network abnormalities, machine crash and other potential problems. As a result, `CSC` introduces penalty mechanism. The slash contract is mainly responsible for keeping track of wrong block records of validator nodes. When the wrong block record reaches a certain threshold, `500 CET` of penalty fee will be taken from the validator's staked assets.

## Rewards

Mainly, the rewards for validators are from block rewards (`1 CET` per block) and commission fees from block transactions. The reward differs according to the proportion of validator staking in overall staking. Since the validator take turns to generates blocks with the same probability (if they remain 100% online), the revenues of all validators are only related to their staking proportion.

The blockchain distributes rewards in proportion to the staking every 200 blocks. Validator's reward receipt address can retrieve the reward by invoking the contract or via [node command line](/validator_cli.md). Rewards can be withdrawed every 28,800 blocks.

## Slash
`CSC` punishes the validator node that fails to produce block normally. All validator nodes take turns to generate blocks. When it is the turn of a node to produce a block but it fails, the wrong block record will be increased by one. Every 200 blocks decreases the wrong block records of all nodes by one. When the wrong block record reaches 48, `500 CET` of penalty fee will be taken from the validator's staked assets. If more than one address has staked to the node, the penalty is proportional to the staking.

You can inquire node's wrong block record by invoking the contract or via [node command line](/validator_cli.md). 
