# 系统合约调用

[csc-genesis-contract](https://github.com/coinex-smart-chain/csc-genesis-contract)

## 合约方法说明

### 1. 验证节点合约

#### 创建验证节点

- method: `create`
- type: transaction(payable)
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | rewardAddr | address | yes | 验证节点收益接收地址 |
    | moniker | str | no | 验证节点昵称 |
    | website | str | no | 验证节点官网 |
    | email | str | no | 验证节点邮箱 |
    | details | str | no | 验证节点描述 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |

#### 编辑验证节点

- method: `edit`
- type: transaction(not payable)
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | rewardAddr | address | yes | 验证节点收益接收地址 |
    | moniker | str | no | 验证节点昵称 |
    | website | str | no | 验证节点官网 |
    | email | str | no | 验证节点邮箱 |
    | details | str | no | 验证节点描述 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |

#### 给验证节点质押

- method: `stake`
- type: transaction(payable)
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |

#### 解除质押

- method: `unstake`
- type: transaction(not payable)
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |

#### 提取质押

- method: `withdrawStaking`
- type: transaction(not payable)
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |

#### 提取出块奖励

- method: `withdrawRewards`
- type: transaction(not payable)
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |

#### 释放出块节点

- method: `unjailed`
- type: transaction(not payable)
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |

#### 查询节点的描述信息

- method: `getValidatorDescription`
- type: call
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | moniker | str | yes | 验证节点昵称 |
    | website | str | yes | 验证节点官网 |
    | email | str | yes | 验证节点邮箱 |
    | details | str | yes | 验证节点描述 |

#### 查询节点的出块及奖励等信息

- method: `getValidatorInfo`
- type: call
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | rewardAddr | address | yes | 验证节点收益接收地址 |
    | status | uint8 | yes | 验证节点状态: NotExist-0, Created-1, Staked-2, Unstake-3, Jailed-4 |
    | stakingAmount | uint256 | yes | 验证节点质押数量 |
    | rewardAmount | uint256 | yes | 验证节点未提取的奖励数量 |
    | slashAmount | uint256 | yes | 验证节点被惩罚的数量 |
    | lastWithdrawRewardBlock | uint256 | yes | 上一次提取奖励的区块高度 |
    | stakers | list | yes | 给该验证节点质押的address列表 |

#### 查询当前出块节点列表

- method: `getActivatedValidators`
- type: call
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validatorSet | list | yes | 当前出块节点address列表 |

#### 查询出块节点候选列表

- method: `getValidatorCandidate`
- type: call
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | candidates | list | yes | 候选出块节点address列表 |
    | stakings | list | yes | 出块节点候选列表对应的质押数量列表(uint256[]) |
    | count | uint256 | yes | 候选出块节点数量 |

#### 获取某个地址对某个验证节点的质押信息

- method: `getStakingInfo`
- type: call
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | staker | address | yes | 质押者地址 |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | amount | uint256 | yes | 该质押人质押到该验证节点的质押数量 |
    | unstakeBlock | uint256 | yes | 执行取回质押交易的区块高度 |
    | index | uint256 | yes | 在验证节点质押人列表中的索引 |

#### 查询某个验证节点是否在当前出块节点列表中

- method: `isValidatorActivated`
- type: call
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | isValidatorActivated | bool | yes | 出块节点是否在当前出块节点列表中 |

#### 查询某个验证节点是否在出块节点候选列表中

- method: `isValidatorCandidate`
- type: call
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | isValidatorCandidate | bool | yes | 出块节点是否在出块节点候选列表中 |

#### 查询某个验证节点是否是Jailed状态

- method: `isJailed`
- type: call
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | isJailed | bool | yes | 出块节点是否是Jailed状态 |

### 2. 惩罚合约

#### 查看出块节点错失的区块数

- method: `getSlashRecord`
- type: call
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | count | uint256 | yes | 错失出块数量 |
