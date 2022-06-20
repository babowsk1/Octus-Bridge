# Base

### StakingPoolBase

#### **`receiveTokenWalletAddress`**

Store vault's token wallet address.  
Only root can call with correct params.

```
function receiveTokenWalletAddress(address wallet) external
```

**Parameters:**

| Name   | Type    | Description          |
|--------|---------|----------------------|
| wallet | address | Token wallet address |

#### **`startNewRewardRound`**

Checks whether there are any rounds if so, sets last round to previous, updates pool about it, adds new round to the list and transfers remaining gas to the address from params.

```
function startNewRewardRound(address send_gas_to) external onlyRewarder
```

**Parameters:**

| Name      | Type    | Description                     |
|-----------|---------|---------------------------------|
| sendGasTo | address | Address where to send spent gas |
|           |         | spent gas                       |

**Events emitted:**
- NewRewardRound

#### **`onAcceptTokensTransfer`**	

Deposit occurs here.

```
function onAcceptTokensTransfer(
        address tokenRoot,
        uint128 amount,
        address sender,
        address senderWallet,
        address remainingGasTo,
        TvmCell payload
    ) external override
```

**Parameters:**

| Name           | Type    | Description                                         |
|----------------|---------|-----------------------------------------------------|
| tokenRoot      | address | Token root address                                  |
| amount         | uint128 | Amount of tokens in transfer                        |
| sender         | address | Address of the sender                               |
| senderWallet   | address | Wallet address of the sender                        |
| remainingGasTo | address | Address where the remaining gas will be transferred |
| payload        | TvmCell | Deposit payload data encoded to Cell                |

**Events emitted:**
- RewardDeposit

#### **`revertDeposit`**	

Reverts the action of depositing.

```
function revertDeposit(uint64 _deposit_nonce) external override
```

**Parameters:**

| Name           | Type   | Description                                |
|----------------|--------|--------------------------------------------|
| _deposit_nonce | uint64 | Id of the deposit which should be reverted |

**Events emitted:**
- DepositReverted

#### **`finishDeposit`**

Finishes the depositing with incrementing token balance for deposit amount.

```
function finishDeposit(uint64 _deposit_nonce) external override
```

**Parameters:**

| Name           | Type   | Description                                 |
|----------------|--------|---------------------------------------------|
| _deposit_nonce | uint64 | Id of the deposit which should be finalized |

**Events emitted:**
- Deposit

#### **`withdraw`**

Withdraw action

```
function withdraw(uint128 amount, address send_gas_to) public onlyActive
```

**Parameters:**

| Name      | Type    | Description                         |
|-----------|---------|-------------------------------------|
| amount    | uint128 | Amount to withdraw                  |
| sendGasTo | address | Address where to send remaining gas |

#### **`finishWithdraw`**	

Finishes the withdrawal with decrementing token balance for deposit amount.

```
function finishWithdraw(
        address user,
        uint128 withdraw_amount,
        address send_gas_to
    ) public override onlyUserData(user)
```

**Parameters:**

| Name            | Type    | Description                         |
|-----------------|---------|-------------------------------------|
| user            | address | User address who initiates withdraw |
| withdraw_amount | uint128 | Amount to withdraw                  |
| sendGasTo       | address | Address where to send remaining gas |

**Events emitted:**
- Withdraw

#### **`claimReward`**	

Claiming reward for user.

```
function claimReward(address send_gas_to) external onlyActive
```

**Parameters:**

| Name      | Type    | Description                         |
|-----------|---------|-------------------------------------|
| sendGasTo | address | Address where to send remaining gas |

#### **`finishClaimReward`**	

Finishes the reward claiming with incrementing user token reward and decrementing reward token balance

```
function finishClaimReward(address user, uint128[] rewards, address send_gas_to) external override onlyUserData(user)
```

**Parameters:**

| Name      | Type      | Description                              |
|-----------|-----------|------------------------------------------|
| user      | address   | Address of the user that claims a reward |
| rewards   | uint128[] | List of rewards                          |
| sendGasTo | address   | Address where to send remaining gas      |

**Events emitted:**
- RewardClaimed

#### **`pendingReward`**

Synchronizes rewards, updates pool info if not empty, gets rewards for old user rounds, synchronizes new user rounds, calculates user reward tokens and returns them.

```
function pendingReward(uint256 user_token_balance, IUserData.RewardRoundData[] user_reward_data) external view responsible returns (uint256)
```

**Parameters:**

| Name               | Type                        | Description                      |
|--------------------|-----------------------------|----------------------------------|
| user_token_balance | uint256                     | Balance of user’s tokens         |
| user_reward_data   | IUserData.RewardRoundData[] | List of all synced user rewards  |

**Returns value:**

| Type    | Description                         |
|---------|-------------------------------------|
| address | Address where to send remaining gas |

updatePoolInfo	
Updates pool information about last reward time and total reward

function updatePoolInfo() internal

#### **`deployUserData`**	

Deploys Platform contract with the user data 

```
function deployUserData(address user_data_owner) internal returns (address)
```

**Parameters:**

| Name            | Type    | Description                          |
|-----------------|---------|--------------------------------------|
| user_data_owner | address | Address of the deployer of user data |

**Returns value:**

| Type    | Description                               |
|---------|-------------------------------------------|
| address | Address of the deployed UserData contract |

#### **`castVoteWithReason`**	

Casts user's vote.

```
function castVote(uint32 proposal_id, bool support) public view override
```

**Parameters:**

| Name        | Type   | Description                               |
|-------------|--------|-------------------------------------------|
| proposal_id | uint32 | Id of the proposal                        |
| support     | bool   | True if voted for, false if voted against |

#### **`castVoteWithReason`**	

Casts user's vote with specified reason

```
function castVoteWithReason(
        uint32 proposal_id,
        bool support,
        string reason
    ) public view override
```

**Parameters:**

| Name        | Type   | Description                               |
|-------------|--------|-------------------------------------------|
| proposal_id | uint32 | Id of the proposal                        |
| support     | bool   | True if voted for, false if voted against |
| reason      | string | Reason for voting                         |

#### **`withdrawTonsUserEmergency`**

User withdraws tons in case of emergency

```
function withdrawTonsUserEmergency() external
```

#### **`withdrawTonsEmergency`**

Checks all the necessary requirements regarding the balance and amount, and does the transfer to the receiver address

```
function withdrawTonsEmergency(uint128 amount, address receiver, bool all, address send_gas_to) external onlyRescuer
```

**Parameters:**

| Name      | Type    | Description                                        |
|-----------|---------|----------------------------------------------------|
| amount    | uint128 | Amount of tons to withdraw                         |
| receiver  | address | Receiver address where tons will be sent           |
| all       | bool    | True if all tons should be withdrawn, false if not |
| sendGasTo | address | Address where to send remaining gas                |

#### **`withdrawTokensEmergency`**	

Tokens withdraw in case of emergency.

```
function withdrawTokensEmergency(uint128 amount, address receiver, bool all, address send_gas_to) external onlyRescuer
```

**Parameters:**

| Name      | Type    | Description                                          |
|-----------|---------|------------------------------------------------------|
| amount    | uint128 | Amount of tokens to withdraw                         |
| receiver  | address | Receiver address where tokens will be sent           |
| all       | bool    | True if all tokens should be withdrawn, false if not |
| sendGasTo | address | Address where to send spent gas                      |

### StakingPoolRelay

#### **`linkRelayAccounts`**

Gets user data and processes linking of relayer eth and ton accounts.

```
function linkRelayAccounts(uint256 ton_pubkey, uint160 eth_address) external view onlyActive
```

**Parameters:**

| Name        | Type    | Description                     |
|-------------|---------|---------------------------------|
| ton_pubkey  | uint256 | Public key of the ton account   |
| eth_address | uint160 | Address of the ethereum account |

#### **`onEventConfirmed`**

Confirms transaction from everscale to ethereum.

```
function onEventConfirmed(
        IEthereumEvent.EthereumEventInitData eventData,
        address gasBackAddress
    ) external override onlyEthTonConfig
```

**Parameters:**

| Name           | Type                                 | Description                         |
|----------------|--------------------------------------|-------------------------------------|
| eventData      | IEthereumEvent.EthereumEventInitData | EthereumEvent data                  |
| gasBackAddress | address                              | Address where to send remaining gas |

#### **`confirmEthAccount`**	

Processes confirmation of ethereum account.

```
function confirmEthAccount(address staker_addr, uint160 eth_address, address send_gas_to) internal
```

**Parameters:**


| Name        | Type    | Description                         |
|-------------|---------|-------------------------------------|
| staker_addr | address | Address of the staker               |
| eth_address | uint160 | Ethereum account address            |
| sendGasTo   | address | Address where to send remaining gas |

#### **`slashRelay`**	

Slashes specified relayer.

```
function slashRelay(address relay_staker_addr, address send_gas_to) external onlyDaoRoot
```

**Parameters:**

| Name              | Type    | Description                                  |
|-------------------|---------|----------------------------------------------|
| relay_staker_addr | address | Address of the relayer which will be slashed |
| sendGasTo         | address | Address where to send remaining gas          |

#### **`_syncUserRewardData`**

Calculates user's reward based on params.

```
function _syncUserRewardData(
        uint128[] user_rewards,
        uint128[] user_debts,
        uint128 ban_token_balance
    ) private view returns (uint128[])
```

**Parameters:**

| Name              | Type      | Description                                                     |
|-------------------|-----------|-----------------------------------------------------------------|
| user_rewards      | uint128[] | List of all user rewards                                        |
| user_debts        | uint128[] | List of all user debts                                          |
| ban_token_balance | uint128   | Used for calculating new user reward that is not already synced |

**Returns value:**

| Type      | Description              |
|-----------|--------------------------|
| uint128[] | Synced user rewards list |

#### **`confirmSlash`**

Confirms slashing by burning gas of slashed user and recalculates round's balance.

function confirmSlash(
        address user,
        uint128[] user_rewards,
        uint128[] user_debts,
        uint128 ban_token_balance,
        address send_gas_to
    ) external override onlyUserData(user)

**Parameters:**

| Name              | Type      | Description                         |
|-------------------|-----------|-------------------------------------|
| user              | address   | Address of the slashed user         |
| user_rewards      | uint128[] | Rewards list of the slashed user    |
| user_debts        | uint128[] | Debts list of the slashed user      |
| ban_token_balance | uint128   | Balance of banned tokens            |
| sendGasTo         | address   | Address where to send remaining gas |

**Events emitted:**
- RelaySlashed

#### **`createOriginRelayRound`**

Creates and deploys new relayer round and sets relayers for that round.

```
function createOriginRelayRound(
        address[] staker_addrs,
        uint256[] ton_pubkeys,
        uint160[] eth_addrs,
        uint128[] staked_tokens,
        uint128 ton_deposit,
        address send_gas_to
    ) external onlyAdmin
```

**Parameters:**

| Name          | Type      | Description                         |
|---------------|-----------|-------------------------------------|
| staker_addrs  | address[] | List of stakers in the round        |
| ton_pubkeys   | uint256[] | List of ton accounts’ public keys   |
| eth_addrs     | uint160[] | List of ethereum’s accounts         |
| staked_tokens | uint128[] | List of staked tokens               |
| ton_deposit   | uint128   | Amount of tons deposited            |
| sendGasTo     | address   | Address where to send remaining gas |
|               |           | remaining gas                       |

#### **`processBecomeRelayNextRound`**	

Processes new relayers for the next relayer round.

```
function processBecomeRelayNextRound(address user) external view override onlyActive onlyUserData(user)
```

**Parameters:**

| Name | Type    | Description                                                           |
|------|---------|-----------------------------------------------------------------------|
| user | address | Address of the user that will be processed for a next round’s relayer |

#### **`processGetRewardForRelayRound`**

Processes rewards for current relayer round.

```
function processGetRewardForRelayRound(address user, uint32 round_num) external override onlyActive onlyUserData(user)
```

**Parameters:**

| Name      | Type    | Description                                      |
|-----------|---------|--------------------------------------------------|
| user      | address | Address of the user that should get a reward     |
| round_num | uint32  | Number of the round for which he will be awarded |

#### **`startElectionOnNewRound`**

Deploys election for a new round.

```
function startElectionOnNewRound() external onlyActive
```

#### **`endElection`**

Based on election's address finishes the current election.

```
function endElection() external onlyActive
```

#### **`onElectionStarted`**

Sets start time of the election.

```
function onElectionStarted(uint32 round_num) external override onlyElection(round_num)
```

**Parameters:**

| Name      | Type   | Description                                |
|-----------|--------|--------------------------------------------|
| round_num | uint32 | Round number in which election has started |

**Events emitted:**
- ElectionStarted

#### **`onElectionEnded`**	

Sets round details and deploys new relayer round.

```
function onElectionEnded(
        uint32 round_num,
        uint32 relay_requests_count
    ) external override onlyElection(round_num)
```

**Parameters:**

| Name                 | Type   | Description                                                                                             |
|----------------------|--------|---------------------------------------------------------------------------------------------------------|
| round_num            | uint32 | Round number in which election has ended                                                                |
| relay_requests_count | uint32 | Number of relayer’s requests (used to check whether there were enough of them for election to be valid) |

**Events emitted:**
- ElectionEnded

#### **`_relaysPacksCount`**	

Returns number of relayer packs.

```
function _relaysPacksCount() private view returns (uint8)
```

**Return value:**

| Type  | Description              |
|-------|--------------------------|
| uint8 | Number of relayers packs |

#### **`onRelayRoundDeployed`**	

Sends relayers to relayer round.

```
function onRelayRoundDeployed(
        uint32 round_num,
        bool duplicate
    ) external override onlyRelayRound(round_num)
```

**Parameters:**

| Name      | Type   | Description               |
|-----------|--------|---------------------------|
| round_num | uint32 | Round number              |
| duplicate | bool   | True if yes, false if not |

#### **`onRelayRoundInitialized`**	

Sets round details, deploys new event and destroys previous round.

```
function onRelayRoundInitialized(
        uint32 round_num,
        uint32 round_start_time,
        uint32 round_end_time,
        uint32 relays_count,
        uint128 round_reward,
        uint32 reward_round_num,
        bool duplicate,
        uint160[] eth_keys
    ) external override onlyRelayRound(round_num)
```

**Parameters:**

| Name             | Type      | Description                                                        |
|------------------|-----------|--------------------------------------------------------------------|
| round_num        | uint32    | Round number                                                       |
| round_start_time | uint32    | Time when the round will start                                     |
| round_end_time   | uint32    | End of the round                                                   |
| relays_count     | uint32    | Number of relayers                                                 |
| round_reward     | uint128   | Reward for the round                                               |
| reward_round_num | uint32    | Number of reward round (index for base_details.rewardRounds array) |
|                  |           | (index for base_details.rewardRounds array)                        |
| duplicate        | bool      | True if yes, false if not                                          |
| eth_keys         | uint160[] | List of ethereum accounts                                          |

**Events emitted:**
- RelayRoundInitialized

#### **`deployElection`**

Creates new platform for the new election.

```
function deployElection(uint32 round_num) private returns (address)
```

**Parameters:**

| Name      | Type   | Description  |
|-----------|--------|--------------|
| round_num | uint32 | Round number |

**Return value:**

| Type    | Description               |
|---------|---------------------------|
| address | Deployed election address |

#### **`deployRelayRound`**

Creates platform for the new relayer round.

```
function deployRelayRound(
        uint32 round_num,
        uint32 start_time,
        uint32 end_time,
        bool duplicate,
        uint8 packs_num,
        address election_addr,
        address prev_relay_round_addr,
        uint16 msg_flag
    ) private returns (address)
```

**Parameters:**

| Name                  | Type    | Description                                    |
|-----------------------|---------|------------------------------------------------|
| round_num             | uint32  | Round number                                   |
| start_time            | uint32  | Round start time                               |
| end_time              | uint32  | Round end time                                 |
| duplicate             | bool    | True if yes, false if not                      |
| packs_num             | uint8   | Number of relayer packs                        |
| election_addr         | address | Address of the election                        |
| prev_relay_round_addr | address | Previous relayer round address                 |
| msg_flag              | uint16  | Flag used for building new RelayRound platform |

**Return value:**

| Type    | Description                       |
|---------|-----------------------------------|
| address | Address of deployed relayer round |

