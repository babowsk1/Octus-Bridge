# Vault

#### **`deposit`**	

Deposits `token` into the Vault, leading to producing corresponding token on the Everscale side.

```
function deposit(
        EverscaleAddress memory recipient,
        uint256 amount
    ) public override onlyEmergencyDisabled
        respectDepositLimit(amount) nonReentrant
```

**Parameters:**

| Name      | Type                    | Description                        |
|-----------|-------------------------|------------------------------------|
| recipient | EverscaleAddress memory | Recipient in the Everscale network |
| amount    | uint256                 | Amount of tokens to deposit        |

**Events emitted:**
- UserDeposit

#### **`deposit`**	

Same as regular `deposit`, but fill multiple pending withdrawals.

```
function deposit(
        EverscaleAddress memory recipient,
        uint256 amount,
        uint256 expectedMinBounty,
        PendingWithdrawalId[] memory pendingWithdrawalIds
    ) external override
```

**Parameters:**

| Name                 | Type                         | Description                          |
|----------------------|------------------------------|--------------------------------------|
| recipient            | EverscaleAddress memory      | Recipient in the Everscale network   |
| amount               | uint256                      | Amount of tokens to deposit          |
| expectedMinBounty    | uint256                      | Expected minimal bounty amount       |
| pendingWithdrawalIds | PendingWithdrawalId[] memory | List of pending withdrawals to close |

**Events emitted:**
- UserDeposit

#### **`depositToFactory`**

Deposits token to Factory.

```
function depositToFactory(
        uint128 amount,
        int8 wid,
        uint256 user,
        uint256 creditor,
        uint256 recipient,
        uint128 tokenAmount,
        uint128 tonAmount,
        uint8 swapType,
        uint128 slippageNumerator,
        uint128 slippageDenominator,
        bytes memory level3
    ) external override onlyEmergencyDisabled respectDepositLimit(amount)
```

**Parameters:**

| Name                | Type         | Description                                    |
|---------------------|--------------|------------------------------------------------|
| amount              | uint128      | Amount to deposit                              |
| wid                 | int8         | Workchain id                                   |
| user                | uint256      | User’s address                                 |
| creditor            | uint256      | Creditor’s address                             |
| recipient           | uint256      | Recipient’s address                            |
| tokenAmount         | uint128      | Token amount                                   |
| tonAmount           | uint128      | Ton amount                                     |
| swapType            | uint8        | Type of swap                                   |
| slippageNumerator   | uint128      | Numerator used in determining slippage value   |
| slippageDenominator | uint128      | Denominator used in determining slippage value |
| level3              | bytes memory |                                                |

**Events emitted:**
- FactoryDeposit

#### **`saveWithdraw`**

Save withdrawal receipt. If Vault has enough tokens and withdrawal passes the limits, then it's executed immediately. Otherwise it's saved as a pending withdrawal.

```
function saveWithdraw(
        bytes memory payload,
        bytes[] memory signatures
    )  public override onlyEmergencyDisabled
        withdrawalNotSeenBefore(payload)
        returns (bool instantWithdrawal, PendingWithdrawalId memory pendingWithdrawalId)
```

**Parameters:**

| Name       | Type           | Description                                           |
|------------|----------------|-------------------------------------------------------|
| payload    | bytes memory   | Withdrawal receipt, bytes encoded from EverscaleEvent |
| signatures | bytes[] memory | List of relay’s signatures                            |

**Return value:**

| Name                | Type                       | Description                                                                   |
|---------------------|----------------------------|-------------------------------------------------------------------------------|
| instantWithdrawal   | bool                       | True if withdrawal was instantly filled, false if saved as pending withdrawal |
| pendingWithdrawalId | PendingWithdrawalId memory | Pending withdrawal Id                                                         |

**Events emitted:**
- InstantWithdrawal

#### **`saveWithdraw`**

Save withdrawal receipt, same as `saveWithdraw(bytes payload, bytes[] signatures)`,but allows to immediately set up bounty.

```
function saveWithdraw(
        bytes memory payload,
        bytes[] memory signatures,
        uint bounty
    )
        external
        override
```

**Parameters:**

| Name       | Type           | Description                                           |
|------------|----------------|-------------------------------------------------------|
| payload    | bytes memory   | Withdrawal receipt, bytes encoded from EverscaleEvent |
| signatures | bytes[] memory | List of relay’s signatures                            |
| bounty     | uint           | New value for pending withdrawal bounty               |

#### **`cancelPendingWithdrawal`**	

Cancel pending withdrawal partially or completely. This may only be called by the pending withdrawal recipient.

```
function cancelPendingWithdrawal(
        uint256 id,
        uint256 amount,
        EverscaleAddress memory recipient,
        uint bounty
    ) external override onlyEmergencyDisabled
        pendingWithdrawalApproved(PendingWithdrawalId(msg.sender, id))
        pendingWithdrawalOpened(PendingWithdrawalId(msg.sender, id))
```

**Parameters:**

| Name      | Type                    | Description                                          |
|-----------|-------------------------|------------------------------------------------------|
| id        | uint256                 | Pending withdrawal Id                                |
| amount    | uint256                 | Amount to cancel (le then pending withdrawal amount) |
| recipient | EverscaleAddress memory | Tokens recipient in Everscale network                |
| bounty    | uint                    | New value for bounty                                 |

**Events emitted:**
- PendingWithdrawalCancel

#### **`withdraw`**

Withdraws the calling account's pending withdrawal from this Vault.

```
function withdraw(
        uint256 id,
        uint256 amountRequested,
        address recipient,
        uint256 maxLoss,
        uint256 bounty
    ) external override onlyEmergencyDisabled
        pendingWithdrawalOpened(PendingWithdrawalId(msg.sender, id))
        pendingWithdrawalApproved(PendingWithdrawalId(msg.sender, id))
        returns(uint256 amountAdjusted)
```

**Parameters:**

| Name            | Type    | Description                                |
|-----------------|---------|--------------------------------------------|
| id              | uint256 | Pending withdrawal Id                      |
| amountRequested | uint256 | Amount of tokens to be withdrawn           |
| recipient       | address | The address to send the redeem tokens      |
| maxLoss         | uint256 | The maximum acceptable loss for withdrawal |
| bounty          | uint256 | New value for bounty                       |

**Return value:**

| Name           | Type    | Description                 |
|----------------|---------|-----------------------------|
| amountAdjusted | uint256 | Quantity of tokens redeemed |

**Events emitted:**
- PendingWithdrawalWithdraw

#### **`addStrategy`**

Add a Strategy to the Vault. This may only be called by `governance`.

```
function addStrategy(
        address strategyId,
        uint256 _debtRatio,
        uint256 minDebtPerHarvest,
        uint256 maxDebtPerHarvest,
        uint256 _performanceFee
    ) external  override onlyGovernance
        onlyEmergencyDisabled strategyNotExists(strategyId)
```

**Parameters:**

| Name              | Type    | Description                                                         |
|-------------------|---------|---------------------------------------------------------------------|
| strategyId        | address | Address of the strategy to add                                      |
| _debtRatio        | uint256 | Share of the total vault’s assets that strategy has access to       |
| minDebtPerHarvest | uint256 | Lower limit on the increase of debt since last harvest              |
| maxDebtPerHarvest | uint256 | Upper limit on the increase of debt since last harvest              |
| _performanceFee   | uint256 | Fee which strategist will receive based on this Vault’s performance |

**Events emitted:**
- StrategyAdded

#### **`updateStrategyDebtRatio`**

Change the quantity of assets `strategy` may manage. This may be called by `governance` or `management`.

```
function updateStrategyDebtRatio(
        address strategyId,
        uint256 _debtRatio
    ) external  override onlyGovernanceOrManagement
        strategyExists(strategyId)
```

**Parameters:**

| Name       | Type    | Description                                         |
|------------|---------|-----------------------------------------------------|
| strategyId | address | Address of the strategy to update                   |
| _debtRatio | uint256 | Quantity of assets strategy may manage after update |

**Events emitted:**
- StrategyUpdateDebtRatio

#### **`updateStrategyMinDebtPerHarvest`**

Updates strategies minimal debt with new value passed from params.

```
function updateStrategyMinDebtPerHarvest(
        address strategyId,
        uint256 minDebtPerHarvest
    ) external override onlyGovernanceOrManagement
        strategyExists(strategyId)
```

**Parameters:**

| Name              | Type    | Description                                            |
|-------------------|---------|--------------------------------------------------------|
| strategyId        | address | Address of the strategy to update                      |
| minDebtPerHarvest | uint256 | Lower limit on the increase of debt since last harvest |

**Events emitted:**
- StrategyUpdateMinDebtPerHarvest

#### **`updateStrategyMaxDebtPerHarvest`**

Updates strategies maximum debt with new value passed from params.

```
function updateStrategyMaxDebtPerHarvest(
        address strategyId,
        uint256 maxDebtPerHarvest
    ) external override onlyGovernanceOrManagement
        strategyExists(strategyId)
```

**Parameters:**

| Name              | Type    | Description                                            |
|-------------------|---------|--------------------------------------------------------|
| strategyId        | address | Address of the strategy to update                      |
| maxDebtPerHarvest | uint256 | Upper limit on the increase of debt since last harvest |

**Events emitted:**
- StrategyUpdateMaxDebtPerHarvest

#### **`updateStrategyPerformanceFee`**

Updates strategies performance fee with new value passed from params.

```
function updateStrategyPerformanceFee(
        address strategyId,
        uint256 _performanceFee
    ) external override onlyGovernance strategyExists(strategyId)
```

**Parameters:**

| Name            | Type    | Description                                                             |
|-----------------|---------|-------------------------------------------------------------------------|
| strategyId      | address | Address of the strategy to update                                       |
| _performanceFee | uint256 | New fee which strategist will receive based on this Vault’s performance |

**Events emitted:**
- StrategyUpdatePerformanceFee

#### **`revokeStrategy`**	

Cancels strategy. 

```
function revokeStrategy(
        address strategyId
    ) external override onlyStrategyOrGovernanceOrGuardian(strategyId)
```

**Parameters:**

| Name       | Type    | Description                       |
|------------|---------|-----------------------------------|
| strategyId | address | Address of the strategy to update |

**Events emitted:**
- StrategyRevoked

#### **`_assessFees`**

Based on the strategy id and reported gain, calculates total fee based on the estimated management, strategist and performance fees.

```
function _assessFees(
        address strategyId,
        uint256 gain
    ) internal returns (uint256)
```

**Parameters:**

| Name       | Type    | Description                            |
|------------|---------|----------------------------------------|
| strategyId | address | Address of the strategy to update      |
| gain       | uint256 | Gains reported used for assessing fees |

**Return value:**

| Type    | Description       |
|---------|-------------------|
| uint256 | New assessed fees |

#### **`report`**

Reports the amount of assets the calling Strategy has free (usually in terms of ROI).

```
function report(
        uint256 gain,
        uint256 loss,
        uint256 _debtPayment
    )
        external
        override
        strategyExists(msg.sender)
        returns (uint256)
```

**Parameters:**

| Name         | Type    | Description                                                                      |
|--------------|---------|----------------------------------------------------------------------------------|
| gain         | uint256 | Amount strategy has realized as a gain on it’s investments since the last report |
| loss         | uint256 | Amount strategy has realized as a loss on it’s investments since the last report |
| _debtPayment | uint256 | Amount strategy has made available to cover outstanding debt                     |

**Return value:**

| Type    | Description                |
|---------|----------------------------|
| uint256 | Amount of debt outstanding |

**Events emitted:**
- StrategyReported

#### **`skim`**

Skim strategy gain to the `rewards_` address. This may only be called by `governance` or `management`. 

```
function skim(
        address strategyId
    ) external  override onlyGovernanceOrManagement
        strategyExists(strategyId)
```

**Parameters:**

| Name       | Type    | Description                       |
|------------|---------|-----------------------------------|
| strategyId | address | Address of the strategy to update |

#### **`skimFees`**

Skim Vault fees to the `rewards_` address. This may only be called by `governance` or `management`.

```
function skimFees(
        bool skim_to_everscale
    ) external override onlyGovernanceOrManagement
```

**Parameters:**

| Name              | Type | Description                                  |
|-------------------|------|----------------------------------------------|
| skim_to_everscale | bool | True if skim fees to Everscale, false if not |

#### **`sweep`**	

Removes tokens from this Vault that are not the type of token managed by this Vault. This may be used in case of accidentally sending the wrong kind of token to this Vault.

```
function sweep(
        address _token
    ) external override onlyGovernance
```

**Parameters:**

| Name   | Type    | Description                                 |
|--------|---------|---------------------------------------------|
| _token | address | Token address to transfer out of this vault |

#### **`forceWithdraw`**

Force user's pending withdrawal. Works only if Vault has enough tokens on its balance.
This may only be called by wrapper.

```
function forceWithdraw(
        PendingWithdrawalId memory pendingWithdrawalId
    )
        public
        override
        onlyEmergencyDisabled
        pendingWithdrawalOpened(pendingWithdrawalId)
        pendingWithdrawalApproved(pendingWithdrawalId)
```

**Parameters:**

| Name                | Type                       | Description           |
|---------------------|----------------------------|-----------------------|
| pendingWithdrawalId | PendingWithdrawalId memory | Pending withdrawal Id |

**Events emitted:**
PendingWithdrawalForce

#### **`forceWithdraw`**	

Multicall for `forceWithdraw`.

```
function forceWithdraw(
        PendingWithdrawalId[] memory pendingWithdrawalId
    ) external override
```

**Parameters:**

| Name                | Type                         | Description           |
|---------------------|------------------------------|-----------------------|
| pendingWithdrawalId | PendingWithdrawalId[] memory | Pending withdrawal Id |

#### **`setPendingWithdrawalApprove`**

Set approve status for pending withdrawal.
Pending withdrawal must be in `Required` (1) approve status, so approve status can be set only once.
If Vault has enough tokens on its balance - withdrawal will be filled immediately.
This may only be called by `governance` or `withdrawGuardian`.

**Events emitted:**
- PendingWithdrawalWithdraw

```
function setPendingWithdrawalApprove(
        PendingWithdrawalId memory pendingWithdrawalId,
        ApproveStatus approveStatus
    ) public override onlyGovernanceOrWithdrawGuardian
        pendingWithdrawalOpened(pendingWithdrawalId)
```

#### **`setPendingWithdrawalApprove`**

Multicall for `setPendingWithdrawalApprove`.

```
function setPendingWithdrawalApprove(
        PendingWithdrawalId[] memory pendingWithdrawalId,
        ApproveStatus[] memory approveStatus
    ) external override
```

**Parameters:**

| Name                | Type                         | Description                                  |
|---------------------|------------------------------|----------------------------------------------|
| pendingWithdrawalId | PendingWithdrawalId[] memory | Pending withdrawal Id                        |
| approveStatus       | ApproveStatus[] memory       | Approve status, must be Approved or Rejected |

#### **`_transferToEverscale`**

Emits event to notify successful transfer.

```
function _transferToEverscale(EverscaleAddress memory recipient,uint256 _amount) internal
```

**Parameters:**

| Name      | Type                    | Description                    |
|-----------|-------------------------|--------------------------------|
| recipient | EverscaleAddress memory | Recipient address in Everscale |
| _amount   | uint256                 | Amount to transfer             |

**Events emitted:**
- Deposit
