# UserData

#### **`propose`**

If user has enough gas and it's not slashed, deploys new proposal to the dao root, if not notifies user that proposal is not created.

```
function propose(
        TvmCell proposal_data,
        uint128 threshold
    ) override public onlyDaoRoot
```

**Parameters:**

| Name          | Type    | Description                                                       |
|---------------|---------|-------------------------------------------------------------------|
| proposal_data | TvmCell | Proposal data in cell format necessary for deploying new proposal |
| threshold     | uint128 | Minimal amount of tokens necessary to propose                     |

#### **`onProposalDeployed`**	

Adds proposal to the created proposals, deletes pending proposal and notifies user that the proposal has been created.

```
function onProposalDeployed(uint32 nonce, uint32 proposal_id, uint32 answer_id) public override onlyDaoRoot
```

**Parameters:**

| Name        | Type   | Description                    |
|-------------|--------|--------------------------------|
| nonce       | uint32 | Id of the temporary proposal   |
| proposal_id | uint32 | The id of the created proposal |
| answer_id   | uint32 |                                |

#### **`castVote`**

If there was an error notifies user that vote is rejected, if not adds vote to the casted votes and casts vote to the proposal with given id.

```
function castVote(uint32 code_version, uint32 proposal_id, bool support, string reason) public override onlyRoot
```

**Parameters:**

| Name         | Type   | Description                                                 |
|--------------|--------|-------------------------------------------------------------|
| code_version | uint32 | Current version of the code                                 |
| proposal_id  | uint32 | The id of the proposal for which user is casting the vote   |
| support      | bool   | True if vote is in favor of proposal, false if it’s against |
| reason       | string | Reason of the decided vote                                  |

**Events emitted:**
- VoteCast

#### **`voteCasted`**	

Notifies user that the vote is casted.

```
function voteCasted(uint32 proposal_id) override public onlyDaoProposal(proposal_id)
```

**Parameters:**

| Name        | Type   | Description                                               |
|-------------|--------|-----------------------------------------------------------|
| proposal_id | uint32 | The id of the proposal for which the users vote is casted |

#### **`rejectVote`**	

Deletes vote from casted votes and notifies user about rejection.

```
function rejectVote(uint32 proposal_id) override public onlyDaoProposal(proposal_id)
```

**Parameters:**

| Name        | Type   | Description                                                 |
|-------------|--------|-------------------------------------------------------------|
| proposal_id | uint32 | The id of the proposal for which the users vote is rejected |

#### **`tryUnlockVoteTokens`**	

Unlocks tokens used for voting.

```
function tryUnlockVoteTokens(uint32 code_version, uint32 proposal_id) override public view onlyRoot
```

**Parameters:**

| Name         | Type   | Description                                                      |
|--------------|--------|------------------------------------------------------------------|
| code_version | uint32 | Current version of the code                                      |
| proposal_id  | uint32 | The id of the proposal for which votes tokens should be unlocked |

#### **`unlockVoteTokens`**

Deletes created proposal and unlocks user votes.

```
function unlockVoteTokens(uint32 proposal_id, bool success) override public onlyDaoProposal(proposal_id)
```

**Parameters:**

| Name        | Type   | Description                                                      |
|-------------|--------|------------------------------------------------------------------|
| proposal_id | uint32 | The id of the proposal for which votes tokens should be unlocked |
| success     | bool   | True if proposal was accepted, false if denied                   |

**Events emitted:**
- UnlockVotes

#### **`tryUnlockCastedVotes`**	

Unlocks casted votes from proposal and transfers remaining gas to user.

```
function tryUnlockCastedVotes(uint32 code_version, uint32[] proposal_ids) override public view onlyRoot
```

**Parameters:**

| Name         | Type     | Description                                                         |
|--------------|----------|---------------------------------------------------------------------|
| code_version | uint32   | Current version of the code                                         |
| proposal_ids | uint32[] | The id’s of the proposals for which casted votes should be unlocked |

#### **`unlockCastedVote`**

Deletes casted votes from list and notifies user that votes are unlocked.

```
function unlockCastedVote(uint32 proposal_id, bool success) override public onlyDaoProposal(proposal_id)
```

**Parameters:**

| Name        | Type   | Description                                         |
|-------------|--------|-----------------------------------------------------|
| proposal_id | uint32 | The id of the proposal for which user casted a vote |
| success     | bool   | True if proposal was accepted, false if denied      |

**Events emitted:**
- UnlockCastedVotes

#### **`_lockedTokens`**

Returns the total amount of user’s locked tokens used in proposals

```
function _lockedTokens() private view returns (uint128)
```

Return value:

| Type    | Description                          |
|---------|--------------------------------------|
| uint128 | Total amount of user’s locked tokens |

#### **`syncRewards`**	

Synchronize all data linked to reward rounds list when adding new reward round.

```
function syncRewards(IStakingPool.RewardRound[] reward_rounds, uint256 updated_balance) internal
```

**Parameters:**

| Name            | Type                       | Description                             |
|-----------------|----------------------------|-----------------------------------------|
| reward_rounds   | IStakingPool.RewardRound[] | List of round’s rewards                 |
| updated_balance | uint256                    | Updated token balance after some action |

#### **`slash`**	

Synchronizes rewards, sets banned rewards, reward debts and token balance and confirms slashing using that data.

```
function slash(IStakingPool.RewardRound[] reward_rounds, address send_gas_to) external override onlyRoot
```

**Parameters:**

| Name          | Type          | Description                     |
|---------------|---------------|---------------------------------|
| reward_rounds | RewardRound[] | List of round’s rewards         |
| send_gas_to   | address       | Address where to send spent gas |

#### **`processDeposit`**

Synchronizes rewards, adds deposited tokens to token balance and finishes deposit.

```
function processDeposit(
        uint64 nonce,
        uint128 _tokens_to_deposit,
        IStakingPool.RewardRound[] reward_rounds,
        uint32 code_version
    ) external override onlyRoot
```

**Parameters:**

| Name               | Type          | Description                                             |
|--------------------|---------------|---------------------------------------------------------|
| nonce              | uint64        | Id of the deposit which should be reverted or finalized |
| _tokens_to_deposit | uint128       | Amount of tokens to deposit                             |
| reward_rounds      | RewardRound[] | List of round’s rewards                                 |
| code_version       | uint32        | Current version of the code                             |

**Events emitted:**
- DepositProcessed

#### **`processClaimReward`**	

Synchronizes rewards, creates new list of rewards whose data is reward balance from each reward round and finishes claiming rewards.

```
function processClaimReward(
        IStakingPool.RewardRound[] reward_rounds,
        address send_gas_to,
        uint32 code_version
    ) external override onlyRoot
```

**Parameters:**

| Name          | Type          | Description                     |
|---------------|---------------|---------------------------------|
| reward_rounds | RewardRound[] | List of round’s rewards         |
| send_gas_to   | address       | Address where to send spent gas |
| code_version  | uint32        | Current version of the code     |

#### **`getRewardForRelayRound`**	

Does all the necessary checks and processes getting the reward for finished relayer round.

```
function getRewardForRelayRound(uint32 round_num) external onlyRelay
```

**Parameters:**

| Name      | Type   | Description         |
|-----------|--------|---------------------|
| round_num | uint32 | Number of the round |

#### **`processGetRewardForRelayRound2`**	

Synchronizes rewards and based on the relayer round address found using round number gets reward for the specified round.

```
function processGetRewardForRelayRound2(
        IStakingPool.RewardRound[] reward_rounds,
        uint32 round_num,
        uint32 code_version,
        uint32 relay_round_code_version
    ) external override onlyRoot
```

**Parameters:**

| Name                     | Type          | Description                       |
|--------------------------|---------------|-----------------------------------|
| reward_rounds            | RewardRound[] | List of round’s rewards           |
| round_num                | uint32        | Number of the round               |
| code_version             | uint32        | Current version of the code       |
| relay_round_code_version | uint32        | Code version of the relay’s round |

#### **`receiveRewardForRelayRound`**	

Increases reward balance for the specified round.

```
function receiveRewardForRelayRound(
        uint32 relay_round_num, uint32 reward_round_num, uint128 reward
    ) external override onlyRelayRound(relay_round_num)
```

**Parameters:**

| Name             | Type     | Description                               |
|------------------|----------|-------------------------------------------|
| relay_round_num  | uint32   | Number of the relayer round               |
| reward_round_num | uint32   | Number of the reward for the round        |
| reward           | uint128  | Amount to increase the reward balance for |

**Events emitted:**
- RelayRoundRewardClaimed

#### **`processLinkRelayAccounts`**

Links relayer accounts by setting the relay_ton_pubkey and relay_eth_address

```
function processLinkRelayAccounts(
        uint256 ton_pubkey,
        uint160 eth_address,
        bool confirm,
        uint32 code_version
    ) external override onlyRoot
```

**Parameters:**

| Name         | Type    | Description                                                      |
|--------------|---------|------------------------------------------------------------------|
| ton_pubkey   | uint256 | Public key of the ton account                                    |
| eth_address  | uint160 | Address of the ethereum account                                  |
| confirm      | bool    | True if both ton and eth accounts are confirmed, false otherwise |
| code_version | uint32  | The current version of the code                                  |

**Events emitted:**
- RelayKeysUpdated
- TonPubkeyConfirmed
- EthAddressConfirmed

#### **`confirmTonAccount`**

Sets ton_pubkey_confirmed to true.

```
function confirmTonAccount() external
```

**Events emitted:**
- TonPubkeyConfirmed

#### **`processConfirmEthAccount`**	

Sets eth_address_confirmed to true and transfers remaining gas to the send_gas_to.

```
function processConfirmEthAccount(uint160 eth_address, address send_gas_to) external override onlyRoot
```

**Parameters:**

| Name        | Type     | Description                     |
|-------------|----------|---------------------------------|
| eth_address | uint160  | Address of the ethereum account |
| send_gas_to | address  | Address where to send spent gas |

**Events emitted:**
- EthAddressConfirmed

#### **`becomeRelayNextRound`**

Processes relayer for next round in the staking pool.

```
function becomeRelayNextRound() external onlyRelay
```

#### **`processBecomeRelayNextRound2`**

Based on election address apply for membership.

```
function processBecomeRelayNextRound2(
        uint32 round_num,
        uint32 lock_time,
        uint128 min_deposit,
        uint32 code_version,
        uint32 election_code_version
    ) external override onlyRoot
```

**Parameters:**

| Name                  | Type     | Description                        |
|-----------------------|----------|------------------------------------|
| round_num             | uint32   | The number of the round            |
| lock_time             | uint32   | Duration of locking the tokens     |
| min_deposit           | uint128  | Minimum amount for relayer deposit |
| code_version          | uint32   | Current version of the code        |
| election_code_version | uint32   | Code version of the election       |

#### **`relayMembershipRequestAccepted`**

Locks relayer for 30 days.

```
function relayMembershipRequestAccepted(
        uint32 round_num, uint128 tokens, uint256 ton_pubkey, uint160 eth_addr, uint32 lock_time
    ) external override onlyElection(round_num)
```

**Parameters:**

| Name       | Type     | Description                     |
|------------|----------|---------------------------------|
| round_num  | uint32   | The number of the round         |
| tokens     | uint128  |                                 |
| ton_pubkey | uint256  | Public key of the ton account   |
| eth_addr   | uint160  | Address of the ethereum account |
| lock_time  | uint32   | Duration of locking the tokens  |

**Events emitted:**
- RelayMembershipRequested

#### **`processWithdraw`**	

Synchronizes rewards, decreases from token balance number of tokens to withdraw and finishes withdraw in the staking pool.

```
function processWithdraw(
        uint128 _tokens_to_withdraw,
        IStakingPool.RewardRound[] reward_rounds,
        bool emergency,
        address send_gas_to,
        uint32 code_version
    ) external override onlyRoot
```

**Parameters:**

| Name                | Type          | Description                                   |
|---------------------|---------------|-----------------------------------------------|
| _tokens_to_withdraw | uint128       | Amount of tokens to withdraw                  |
| reward_rounds       | RewardRound[] | List of round’s rewards                       |
| emergency           | bool          | True if withdrawal is emergency, false if not |
| send_gas_to         | address       | Address where to send spent gas               |
| code_version        | uint32        | Current version of the code                   |

#### **`withdrawTons`**

Transfers to user all the tons left.

```
function withdrawTons() external override onlyRoot
```