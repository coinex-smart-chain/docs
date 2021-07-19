# 系统合约调用

[csc-genesis-contract](https://github.com/coinex-smart-chain/csc-genesis-contract)

## 合约方法说明

### 1. 验证节点合约

#### 创建验证节点

- name: `create`
- type: transaction(payable)
- method: `function create(address payable rewardAddr, string calldata moniker, string calldata website, string calldata email, string calldata details) external payable onlyInitialized returns (bool) `
- conditions: 
  1. 该地址的验证者未被创建；
  2. rewardAddr是非零地址；
  3. 其他参数有效，moniker小于128字节、website小于256字节、email小于256字节、details小于1024字节。
- actions: 
  1. 创建验证者；
  2. 如果交易的value值超过10000`CET`，则将同步完成质押操作；
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
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | ValidatorCreated | `ValidatorCreated(address indexed validator, address indexed rewardAddr)` | yes | 创建验证节点 |
    | Staking | `Staking(address indexed staker, address indexed validator, uint256 amount)` | no | 质押 |

#### 编辑验证节点

- name: `edit`
- type: transaction(not payable)
- method: `function edit(address payable rewardAddr, string calldata moniker, string calldata website, string calldata email, string calldata details) external onlyInitialized returns (bool) `
- conditions: 
  1. 该地址的验证者已被创建；
  2. rewardAddr是非零地址；
  3. 其他参数有效，moniker小于128字节、website小于256字节、email小于256字节、details小于1024字节。
- actions: 
  1. 更新验证者的rewardAddr、moniker、website、email、details信息。
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
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | ValidatorUpdated | `ValidatorUpdated(address indexed validator, address indexed rewardAddr)` | yes | 更新验证节点信息 |

#### 给验证节点质押

- name: `stake`
- type: transaction(payable)
- method: `function stake(address validator) external payable onlyInitialized returns (bool)`
- conditions: 
  1. 该地址的验证者已被创建；
  2. 当前不在该质押者到该验证者的unstaking状态；
  3. 质押数量必须超过1000`CET`；
  4. 质押后验证者的总质押数量必须超过10000`CET`。
- actions: 
  1. 给验证者质押，如果验证者不在候选出块节点集合中，将其加入。
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | Staking | `Staking(address indexed staker, address indexed validator, uint256 amount)` | yes | 质押 |

#### 解除质押

- name: `unstake`
- type: transaction(not payable)
- method: `function unstake(address validator) external onlyInitialized returns (bool)`
- conditions: 
  1. 该地址的验证者已被创建；
  2. 当前不在该质押者到该验证者的unstaking状态；
  3. 你质押到该验证者的数量大于0。
- actions: 
  1. 解除给某个验证者的质押，如果该验证者的总质押数量小于10000`CET`，将其从候选出块节点集合中踢出。
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | Unstake | `Unstake(address indexed staker, address indexed validator, uint256 amount, uint256 unLockHeight)` | yes | 解除质押 |

#### 提取质押

- name: `withdrawStaking`
- type: transaction(not payable)
- method: `function withdrawStaking(address validator) external returns (bool)`
- conditions: 
  1. 该地址的验证者已被创建；
  2. 当前处于该质押者到该验证者的unstaking状态，即已经执行了解除质押操作；
  3. 质押已经解锁，即距离解除质押交易所在区块已超过86400个区块；
  4. 你质押到该验证者的数量大于0。
- actions: 
  1. 提取质押给某个验证者的所有质押。
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | WithdrawStaking | `WithdrawStaking(address indexed staker, address indexed validator, uint256 amount)` | yes | 提取质押 |

#### 提取出块奖励

- name: `withdrawRewards`
- type: transaction(not payable)
- method: `function withdrawRewards(address validator) external returns (bool)`
- conditions: 
  1. 该地址的验证者已被创建；
  2. 交易发起者地址和该验证者设置的rewardAddr一致；
  3. 距离上次提取出块奖励已超过86400个区块；
  4. 待提取的奖励数量大于0。
- actions: 
  1. 提取出块奖励。
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | WithdrawRewards | `WithdrawRewards(address indexed validator, address indexed rewardAddress, uint256 amount, uint256 nextWithdrawBlock)` | yes | 提取出块奖励 |

#### 释放出块节点

- name: `unjailed`
- type: transaction(not payable)
- method: `function unjailed() external onlyInitialized returns (bool)`
- conditions: 
  1. 交易发起者是已创建的验证者，且该验证者的状态为Jailed。
- actions: 
  1. 调用Slash合约的`clean`方法，清除节点错块记录；
  2. 如果该验证者的总质押数量超过10000`CET`，将其加入候选出块节点集合。
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | 是否执行成功 |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | ValidatorUnjailed | `ValidatorUnjailed(address indexed validator)` | yes | 释放出块节点 |

#### 查询节点的描述信息

- name: `getValidatorDescription`
- type: call
- method: `function getValidatorDescription(address validator) public view returns (string memory, string memory, string memory, string memory)`
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

- name: `getValidatorInfo`
- type: call
- method: `function getValidatorInfo(address validator) public view returns (address payable, Status, uint256, uint256, uint256, uint256, address[] memory)`
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

- name: `getActivatedValidators`
- type: call
- method: `function getActivatedValidators() public view returns (address[] memory)`
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validatorSet | list | yes | 当前出块节点address列表 |

#### 查询出块节点候选列表

- name: `getValidatorCandidate`
- type: call
- method: `function getValidatorCandidate() public view returns (address[] memory, uint256[] memory, uint256)`
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | candidates | list | yes | 候选出块节点address列表 |
    | stakings | list | yes | 出块节点候选列表对应的质押数量列表(uint256[]) |
    | count | uint256 | yes | 候选出块节点数量 |

#### 获取某个地址对某个验证节点的质押信息

- name: `getStakingInfo`
- type: call
- method: `function getStakingInfo(address staker, address validator) public view returns (uint256, uint256, uint256)`
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

- name: `isValidatorActivated`
- type: call
- method: `function isValidatorActivated(address validator) public view returns (bool)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | isValidatorActivated | bool | yes | 出块节点是否在当前出块节点列表中 |

#### 查询某个验证节点是否在出块节点候选列表中

- name: `isValidatorCandidate`
- type: call
- method: `function getActivatedValidators() public view returns (address[] memory)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | isValidatorCandidate | bool | yes | 出块节点是否在出块节点候选列表中 |

#### 查询某个验证节点是否是Jailed状态

- name: `isJailed`
- type: call
- method: `function isJailed(address validator) public view returns (bool)`
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

- name: `getSlashRecord`
- type: call
- method: `function getSlashRecord(address validator) public view returns (uint256)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | 验证节点地址 |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | count | uint256 | yes | 错失出块数量 |
