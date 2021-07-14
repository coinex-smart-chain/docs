# CSC Validator

## What is Validator

`CSC` adopts ['CPoS'](/en-us/consensus.md) consensus and supports up to 101 validators. In order, each validator takes turn to generate blocks and validate block info of other validators.

## How to become a validator

Everyone can become validator by staking `CET`. Based on overall staking ranking, the blockchain will select the top 101 nodes as validators in every 200 blocks.

## How to stake
 
After launch, `CSC` will initialize the validator system contract. Staking is available for everyone via invoking the contract directly. The first staking for the validator must exceed 10000CET and each subsequent staking must exceed 1000CET. In addition to stake by invoking the contract directly, you can also stake via node command line. More details of [Validator CLI](/en-us/validator_cli.md)

## Rewards

Mainly, the rewards for validators are from block rewards and tx fees. These rewards will be allocated according to the proportion of node staking in overall staking.
