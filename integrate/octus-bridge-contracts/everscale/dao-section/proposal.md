# Proposal

#### **`queue`**	

Happening after proposal execution

```
function queue() override public
```

**Events emitted:**
- Queued

#### **`execute`**

Proposal execution.

```
function execute() override public
```

**Events emitted:**
- Executed

#### **`cancel`**	

Proposal cancel.

```
function cancel() override public
```

**Events emitted:**
- Canceled


#### **`castVote`**

Processing voter's vote is it for or against proposal.

```
function castVote(
        uint32 /*proposalId*/,
        address voter,
        uint128 votes,
        bool support,
        string reason
    ) override public onlyStakingAccount(voter)
```

**Parameters:**

| Name    | Type     | Description                               |
|---------|----------|-------------------------------------------|
|         | uint32   | The id of the proposal                    |
| voter   | address  | The address of the voter                  |
| votes   | uint128  | Number of votes given for proposal        |
| support | bool     | True if voting in favor, false if against |
| reason  | string   | Reason of the decided vote                |

**Events emitted:**
- VoteCast

#### **`onActionsExecuted`**

Callback for executed actions.

```
function onActionsExecuted() override public onlyRoot
```

#### **`state`**

Gets the state of the proposal based on the specified conditions.

```
function state() private view returns (ProposalState)
```

**Return values:**

| Type          | Description            |
|---------------|------------------------|
| ProposalState | Current proposal state |

#### **`unlockCastedVote`**

Unlocks casted vote only if proposal state is not active.

```
function unlockCastedVote(address accountOwner) override public view onlyStakingAccount(accountOwner)
```

**Parameters:**

| Name         | Type    | Description                      |
|--------------|---------|----------------------------------|
| accountOwner | address | The address of the account owner |

#### **`unlockVoteTokens`**

Unlocks vote tokens based on the proposal state.

```
function unlockVoteTokens(address accountOwner) override public view onlyStakingAccount(accountOwner)
```

**Parameters:**

| Name         | Type    | Description                      |
|--------------|---------|----------------------------------|
| accountOwner | address | The address of the account owner |

#### **`_buildAccountInitialData`**

Builds initial data for account.

```
function _buildAccountInitialData(address accountOwner) private inline pure returns (TvmCell)
```

**Parameters:**

| Name         | Type    | Description                      |
|--------------|---------|----------------------------------|
| accountOwner | address | The address of the account owner |

**Return values:**

| Type    | Description                         |
|---------|-------------------------------------|
| TvmCell | Account initial data in cell format |

#### **`_buildStakingInitData`**

Builds initial data for staking.

```
function _buildStakingInitData(uint8 platformType, TvmCell initialData) private inline view returns (TvmCell)
```

**Parameters:**

| Name         | Type     | Description                             |
|--------------|----------|-----------------------------------------|
| platformType | uint8    | The type of the platform                |
| initialData  | TvmCell  | Initial data represented in cell format |

**Return values:**

| Type    | Description                         |
|---------|-------------------------------------|
| TvmCell | Staking initial data in cell format |

#### **`requestUpgrade`**

Creates request for upgrading proposal for different version

```
function requestUpgrade(address sendGasTo) override public view
```

**Parameters:**

| Name      | Type    | Description                     |
|-----------|---------|---------------------------------|
| sendGasTo | address | Address where to send spent gas |

**Events emitted:**
- CodeUpgradeRequested

#### **`upgrade`**

Upgrades code to the new version

```
function upgrade(TvmCell code, uint16 newVersion, address sendGasTo) override public onlyRoot
```

**Parameters:**

| Name       | Type     | Description                         |
|------------|----------|-------------------------------------|
| code       | TvmCell  | Code to be set for upgraded version |
| newVersion | uint16   | New version of the code             |
| sendGasTo  | address  | Address where to send spent gas     |

**Events emitted:**
- ProposalCodeUpgraded

