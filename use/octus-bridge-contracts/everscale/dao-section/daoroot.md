# DAORoot

#### **`propose`**

Creates new DAO proposal.

```
function propose(
        uint32 answerId,
        TonAction[] tonActions,
        EthAction[] ethActions,
        string description
    ) override public
```

**Parameters:**

| Name        | Type        | Description                 |
|-------------|-------------|-----------------------------|
| answerId    | uint32      |                             |
| tonActions  | TonAction[] | List of everscale actions   |
| ethActions  | EthAction[] | List of ethereum actions    |
| description | string      | Description of the proposal |

#### **`deployProposal`**	

Deploys Proposal contract (creates a new instance of Platform contract).

```
function deployProposal(
        uint32 nonce,
        address accountOwner,
        TvmCell proposalData
    ) override public onlyStakingAccount(accountOwner)onProposalDeployed
```

| Name         | Type     | Description                                                                                   |
|--------------|----------|-----------------------------------------------------------------------------------------------|
| nonce        | uint32   |                                                                                               |
| accountOwner | address  | The address of owner of the account                                                           |
| proposalData | TvmCell  | Information about the proposal, including answer id, description, list of TON and EVM actions |

**Events emitted:**
- ProposalCreated

#### **`onProposalSucceeded`**

Callback method after successful proposal.

```
function onProposalSucceeded(
        uint32 proposalId,
        address proposer,
        TonAction[] tonActions,
        EthAction[] ethActions
    ) override public onlyProposal(proposalId)
```

**Parameters:**

| Name       | Type        | Description                     |
|------------|-------------|---------------------------------|
| proposalId | uint32      | The id of the proposal          |
| proposer   | address     | Address of the proposal creator |
| tonActions | TonAction[] | List of everscale actions       |
| ethActions | EthAction[] | List of ethereum actions        |

**Events emitted:**
- ExecutingTonActions

#### **`executeTonAction`**	

Does the transfer based on the action payload.

```
function executeTonAction(TonAction action) private pure inline
```

**Parameters:**

| Name   | Type      | Description                         |
|--------|-----------|-------------------------------------|
| action | TonAction | The everscale action to be executed |

#### **`executeEthActions`**

Based on the list of actions fills necessary data, adds actions to the chain of actions, encodes them to the event data and deploys events.

```
function executeEthActions(address proposer, EthAction[] actions) private view inline
```
**Parameters:**

| Name     | Type        | Description                        |
|----------|-------------|------------------------------------|
| proposer | address     | Address of the proposal creator    |
| actions  | EthAction[] | The ethereum action to be executed |

#### **`calcTonActionsValue`**	

Calculates total value of actions on Everscale.

```
function calcTonActionsValue(TonAction[] actions) public pure returns (uint128 totalValue)
```

Parameters:

| Name    | Type        | Description                          |
|---------|-------------|--------------------------------------|
| actions | TonAction[] | The list of actions to be calculated |

**Return values:**

| Name       | Type    | Description                     |
|------------|---------|---------------------------------|
| totalValue | uint128 | Total value of the actions list |

#### **`calcEthActionsValue`**

Calculates total value of actions on Ethereum.

```
function calcEthActionsValue(
        EthAction[] actions
    ) public view returns (uint128 totalValue)
```

**Parameters:**

| Name    | Type        | Description                          |
|---------|-------------|--------------------------------------|
| actions | EthAction[] | The list of actions to be calculated |

**Return values:**

| Name       | Type    | Description                     |
|------------|---------|---------------------------------|
| totalValue | uint128 | Total value of the actions list |

_buildProposalInitialData	
Builds initial data for Proposal

function _buildProposalInitialData(uint32 proposalId) private inline pure returns (TvmCell)

**Parameters:**

| Name       | Type   | Description            |
|------------|--------|------------------------|
| proposalId | uint32 | The id of the proposal |

**Return values:**

| Type    | Description                          |
|---------|--------------------------------------|
| TvmCell | Proposal initial data in cell format |

#### **`_buildStakingAccountInitialData`**	

Builds initial data for Staking account

```
function _buildStakingAccountInitialData(address accountOwner) private inline pure returns (TvmCell)
```
**Parameters:**

| Name         | Type    | Description                              |
|--------------|---------|------------------------------------------|
| accountOwner | address | The address of the staking account owner |

**Return values:**

| Type    | Description                                 |
|---------|---------------------------------------------|
| TvmCell | Staking account initial data in cell format |

#### **`_buildInitData`**

Builds initial data for specified Platform type.

```
function _buildInitData(PlatformType platformType, TvmCell initialData) private view returns (TvmCell)
```

**Parameters:**

| Name         | Type         | Description                              |
|--------------|--------------|------------------------------------------|
| platformType | PlatformType | Type of the platform                     |
| initialData  | TvmCell      | The proposal initial data in cell format |

**Return values:**

| Type    | Description                             | Description          |
|---------|-----------------------------------------|----------------------|
| TvmCell | Initial data represented in cell format | Type of the platform |

#### **`requestUpgradeProposal`**	

Creates request for upgrading proposal for different version.

```
function requestUpgradeProposal(
        uint16 currentVersion,
        address sendGasTo,
        uint32 proposalId
    ) override public onlyProposal(proposalId)
```

**Parameters:**

| Name           | Type     | Description                     |
|----------------|----------|---------------------------------|
| currentVersion | uint16   | Current version of proposal     |
| sendGasTo      | address  | Address where to send spent gas |
| proposalId     | uint32   | The id of the proposal          |

#### **`setStakingRoot`**	

Sets staking root address from params and transfers remaining gas to admin

```
function setStakingRoot(address newStakingRoot) override public onlyAdmin
```

**Parameters:**

| Name           | Type    | Description                         |
|----------------|---------|-------------------------------------|
| newStakingRoot | address | The address of the new staking root |

**Events emitted:**
- StakingRootUpdated

#### **`transferAdmin`**	

Transfers admin role to other address.

```
function transferAdmin(address newAdmin) override public onlyAdmin
```

**Parameters:**

| Name     | Type    | Description                  |
|----------|---------|------------------------------|
| newAdmin | address | The address of the new admin |

**Events emitted:**
- AdminTransferAccepted