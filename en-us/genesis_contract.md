# Genesis Contract

[csc-genesis-contract](https://github.com/coinex-smart-chain/csc-genesis-contract)

## Method Statement

### 1. Validator Contract

#### Create validator

- name: `create`
- type: transaction(payable)
- method: `function create(address payable rewardAddr, string calldata moniker, string calldata website, string calldata email, string calldata details) external payable onlyInitialized returns (bool) `
- conditions: 
  1. A validator for this address has not been created;
  2. RewardAddr is a non-zero address;
  3. Other parameters are valid, moniker < 128 bytes, website < 256 bytes, email < 256 bytes, details < 1024 bytes.
- actions: 
  1. Create validator;
  2. If the value of the transaction exceeds `10000 CET`, the stake operation will be completed simultaneously.
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | rewardAddr | address | yes | reward address |
    | moniker | str | no | moniker |
    | website | str | no | website |
    | email | str | no | email |
    | details | str | no | details |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | success |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | ValidatorCreated | `ValidatorCreated(address indexed validator, address indexed rewardAddr)` | yes | create validator |
    | Staking | `Staking(address indexed staker, address indexed validator, uint256 amount)` | no | stake |

#### Edit validator

- name: `edit`
- type: transaction(not payable)
- method: `function edit(address payable rewardAddr, string calldata moniker, string calldata website, string calldata email, string calldata details) external onlyInitialized returns (bool) `
- conditions: 
  1. A validator for this address has been created;
  2. RewardAddr is a non-zero address;
  3. Other parameters are valid, moniker < 128 bytes, website < 256 bytes, email < 256 bytes, details < 1024 bytes.
- actions: 
  1. Update the validator's rewardAddr, moniker, website, email, and details.
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | rewardAddr | address | yes | reward address |
    | moniker | str | no | moniker |
    | website | str | no | website |
    | email | str | no | email |
    | details | str | no | details |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | success |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | ValidatorUpdated | `ValidatorUpdated(address indexed validator, address indexed rewardAddr)` | yes | update validator |

#### Stake

- name: `stake`
- type: transaction(payable)
- method: `function stake(address validator) external payable onlyInitialized returns (bool)`
- conditions: 
  1. A validator for this address has been created;
  2. The status is not unstaking from the staker to the validator right now;
  3. The amount of staking must exceed `1000 CET`;
  4. After staking, the amount of the validator's total staking must exceed `10000 CET`.
- actions: 
  1. Stake for the validator to join the candidate validator list if the validator is not in it.
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | success |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | Staking | `Staking(address indexed staker, address indexed validator, uint256 amount)` | yes | stake |

#### Unstake

- name: `unstake`
- type: transaction(not payable)
- method: `function unstake(address validator) external onlyInitialized returns (bool)`
- conditions: 
  1. A validator for this address has been created;
  2. The status is not unstaking from the staker to the validator right now;
  3. The amount of staking you staked to the validator is greater than 0.
- actions: 
  1. Unstake from the validator, if the amount of the validator's total staking less than `10000 CET`, kick it out of the candidate validator list.
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | success |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | Unstake | `Unstake(address indexed staker, address indexed validator, uint256 amount, uint256 unLockHeight)` | yes | unstake |

#### Withdraw staking

- name: `withdrawStaking`
- type: transaction(not payable)
- method: `function withdrawStaking(address validator) external returns (bool)`
- conditions: 
  1. A validator for this address has been created;
  2. The status is unstaking from the staker to the validator. That is, you have unstaked from the validator;
  3. The staking has been unlocked, that is, there are more than 86,400 blocks from your unstaking operation;
  4. The amount of staking you staked to the validator is greater than 0.
- actions: 
  1. Withdraw all stakings staked to a validator.
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | success |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | WithdrawStaking | `WithdrawStaking(address indexed staker, address indexed validator, uint256 amount)` | yes | withdraw staking |

#### Withdraw rewards

- name: `withdrawRewards`
- type: transaction(not payable)
- method: `function withdrawRewards(address validator) external returns (bool)`
- conditions: 
  1. A validator for this address has been created;
  2. The address who create this transaction is the same as the rewardAddr set by the validator;
  3. It has been over 28,800 blocks since you last withdraw the reward;
  4. The number of rewards to be withdrew is greater than 0.
- actions: 
  1. Withdraw rewards.
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | success |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | WithdrawRewards | `WithdrawRewards(address indexed validator, address indexed rewardAddress, uint256 amount, uint256 nextWithdrawBlock)` | yes | withdraw rewards |

#### Unjail node

- name: `unjailed`
- type: transaction(not payable)
- method: `function unjailed() external onlyInitialized returns (bool)`
- conditions: 
  1. The creator of the transaction is a created validator, and the validator was in a 'Jailed' state.
- actions: 
  1. Invoke the `clean` method of the Slash contract to clear the node's wrong block record;
  2. If the amount of the validator's total staking is more than `10000 CET`, add it to the candidate validator list.
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | success | bool | yes | success |
- event:
    | name | event | must | description |
    | :--- | :--- | :--- | :--- |
    | ValidatorUnjailed | `ValidatorUnjailed(address indexed validator)` | yes | unjail node |

#### Inquire validator description info

- name: `getValidatorDescription`
- type: call
- method: `function getValidatorDescription(address validator) public view returns (string memory, string memory, string memory, string memory)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | moniker | str | yes | moniker |
    | website | str | yes | website |
    | email | str | yes | email |
    | details | str | yes | details |

#### Inquire node info such as block generation, reward, etc

- name: `getValidatorInfo`
- type: call
- method: `function getValidatorInfo(address validator) public view returns (address payable, Status, uint256, uint256, uint256, uint256, address[] memory)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | rewardAddr | address | yes | reward address |
    | status | uint8 | yes | validator status: NotExist-0, Created-1, Staked-2, Unstake-3, Jailed-4 |
    | stakingAmount | uint256 | yes | number of staking amount |
    | rewardAmount | uint256 | yes | number of undrawn rewards |
    | slashAmount | uint256 | yes | number of slash |
    | lastWithdrawRewardBlock | uint256 | yes | block number when withdraw reward last time |
    | stakers | list | yes | the address list staked to the validator |

#### Inquire activated node list

- name: `getActivatedValidators`
- type: call
- method: `function getActivatedValidators() public view returns (address[] memory)`
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validatorSet | list | yes | the address list of the current block producing node |

#### Inquire candidate node list

- name: `getValidatorCandidate`
- type: call
- method: `function getValidatorCandidate() public view returns (address[] memory, uint256[] memory, uint256)`
- params: 
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | candidates | list | yes |  the address list of candidate nodes |
    | stakings | list | yes | the staking number list that corresponds to candidate nodes list (uint256[]) |
    | count | uint256 | yes | length of candidate nodes list |

#### Inquire staking info from any address to node

- name: `getStakingInfo`
- type: call
- method: `function getStakingInfo(address staker, address validator) public view returns (uint256, uint256, uint256)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | staker | address | yes | the address of staker |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | amount | uint256 | yes | staking amount |
    | unstakeBlock | uint256 | yes | the block number when excute withdraw staking transaction |
    | index | uint256 | yes | index in the staker list of the validator |

#### Inquire whether a validator is in the current block-producing node list

- name: `isValidatorActivated`
- type: call
- method: `function isValidatorActivated(address validator) public view returns (bool)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | isValidatorActivated | bool | yes | whether a validator is in the current block-producing node list |

#### Inquire whether a validator is in the candidate list

- name: `isValidatorCandidate`
- type: call
- method: `function getActivatedValidators() public view returns (address[] memory)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | isValidatorCandidate | bool | yes | whether a validator is in the candidate list |

#### Inquire whether a particular validator is a Jailed state

- name: `isJailed`
- type: call
- method: `function isJailed(address validator) public view returns (bool)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | isJailed | bool | yes | whether a validator is in Jailed state |

### 2. Slash Contract

#### Inquire validator penalty record

- name: `getSlashRecord`
- type: call
- method: `function getSlashRecord(address validator) public view returns (uint256)`
- params: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | validator | address | yes | the address of validator |
- result: 
    | name | type | required | description |
    | :--- | :--- | :--- | :--- |
    | count | uint256 | yes | number of missed blocks |
