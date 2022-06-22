# ConvexCrvLp

#### **`withdrawToConvexDepositTokens`**	

Withdraws all tokens from reward contract.

```
function withdrawToConvexDepositTokens() external onlyAuthorized
```

#### **`withdrawToWrappedTokens`**	

Withdraws all tokens from reward contract and unwraps them.

```
function withdrawToWrappedTokens() external onlyAuthorized
```

#### **`claimWantTokens`**	

Transfers unwrapped want tokens to governance. Can be only called by governance.

```
function claimWantTokens() external onlyGovernance
```

#### **`claimWrappedWantTokens`**	

Transfers wrapped want tokens to governance. Can be called only by governance.

```
function claimWrappedWantTokens() external onlyGovernance
```

#### **`claimRewardTokens`**	

Transfers reward tokens (crv and cvx) to governance. Can be called only by governance.

```
function claimRewardTokens() external onlyGovernance
```

#### **`name`**	

Returns string representation of abi file of the wanted wrapped token symbol.

```
function name() external view override returns (string memory)
```

**Return value:**

| Type          | Description                    |
|---------------|--------------------------------|
| string memory | Symbol of wanted wrapped token |

#### **`calc_want_from_wrapped`**	

If amount of want tokens is greater than 0 returns calculated amount of wrapped tokens.

```
function calc_want_from_wrapped(uint256 wrapped_amount) public virtual view returns (uint256 expected_return)
```

**Parameters:**

| Name           | Type    | Description                               |
|----------------|---------|-------------------------------------------|
| wrapped_amount | uint256 | Amount of wrapped tokens to be calculated |

**Return value:**

| Name            | Type    | Description                                   |
|-----------------|---------|-----------------------------------------------|
| expected_return | uint256 | Amount of want tokens calculated from wrapped |

#### **`unwrap`**	

Returns amount of wanted tokens after unwrapping and removes wrapped amount from curve's pool. 

```
function unwrap(uint256 wrapped_amount) internal virtual returns (uint256 expected_return)
```

**Parameters:**

| Name           | Type    | Description                              |
|----------------|---------|------------------------------------------|
| wrapped_amount | uint256 | Amount of wrapped tokens to be unwrapped |

**Return value:**

| Name            | Type    | Description                       |
|-----------------|---------|-----------------------------------|
| expected_return | uint256 | Amount of tokens after unwrapping |

#### **`balanceOfWant`**

Returns balance of want tokens from the caller of the contract.

```
function balanceOfWant() public view returns (uint256)
```

**Return value:**

| Type    | Description           |
|---------|-----------------------|
| uint256 | Amount of want tokens |

#### **`estimatedTotalAssets`**

Returns amount of total wrapped and want tokens.

```
function estimatedTotalAssets() public view override returns (uint256)
```

**Parameters:**

| Type    | Description                             |
|---------|-----------------------------------------|
| uint256 | Amount of total wrapped and want tokens |

#### **`adjustPosition`**	

Calculates total available tokens and if it's greater than the minimum debt it wraps the want tokens and deposits them to booster.

```
function adjustPosition(uint256 /*_debtOutstanding*/) internal override
```

**Parameters:**

| Type    | Description                  |
|---------|------------------------------|
| uint256 | Value of the unwrapped token |

#### **`_withdrawSome`**	

Withdraws and unwraps reward amount and returns new balance of wrapped tokens after withdraw.

```
function _withdrawSome(uint256 _amount) internal returns (uint256)
```

**Parameters:**

| Name    | Type    | Description                  |
|---------|---------|------------------------------|
| _amount | uint256 | Amount of tokens to withdraw |

**Return value:**

| Type    | Description                              |
|---------|------------------------------------------|
| uint256 | Balance of wrapped tokens after withdraw |

#### **`liquidatePosition`**

Returns liquidated amount and loss, if balance is less than amount needed to withdraw, loss is calculated for further actions (throwing an error for example).

```
function liquidatePosition(uint256 _amountNeeded) internal override returns (uint256 _liquidatedAmount, uint256 _loss)
```

**Parameters:**

| Name          | Type    | Description                               |
|---------------|---------|-------------------------------------------|
| _amountNeeded | uint256 | Amount of wrapped tokens to be liquidated |

**Return value:**

| Name              | Type    | Description                                     |
|-------------------|---------|-------------------------------------------------|
| _liquidatedAmount | uint256 | Amount of liquidated tokens                     |
| _loss             | uint256 | Loss after liquidating (should be 0, o/w error) |

#### **`prepareMigration`**	

Withdraws and unwraps all the reward tokens, migrates rewards based on new strategy and transfers balance of wrapped tokens to the want wrapped token pool.

```
function prepareMigration(address _newStrategy) internal override
```

**Parameters:**

| Name         | Type    | Description                  |
|--------------|---------|------------------------------|
| _newStrategy | address | New strategy’s vault address |

#### **`_migrateRewards`**	

Transfers all the curve and convex tokens from this contract's pool to their pool's address.

```
function _migrateRewards(address _newStrategy) internal virtual
```

**Parameters:**

| Name         | Type    | Description              |
|--------------|---------|--------------------------|
| _newStrategy | address | Strategy’s vault address |

#### **`_claimableBasicInETH`**	

Takes curve amount from this pool, calculates convex amount based on it, afterwards calculates convex and curve's value and returns their sum when swapped to ETH.

```
function _claimableBasicInETH() internal view returns (uint256)
```

**Return value:**

| Type    | Description                                   |
|---------|-----------------------------------------------|
| uint256 | Sum of convex and curve tokens swapped to eth |

#### **`claimableInETH`**	

Returns claimable value.

```
function claimableInETH() public virtual view returns (uint256 _claimable)
```

**Return value:**

| Name       | Type    | Description                    |
|------------|---------|--------------------------------|
| _claimable | uint256 | Amount of claimable ETH tokens |

#### **`harvestTrigger`**

Decides whether harvest should be triggered based on numerous factors (minReportDelay, maxReportDelay, totalDebt...), returns true if yes, false if not.

```
function harvestTrigger(uint256 callCost) public override view returns (bool)
```

**Parameters:**

| Name     | Type    | Description                 |
|----------|---------|-----------------------------|
| callCost | uint256 | Fee for triggering harvest  |

**Return value:**

| Type | Description                                  |
|------|----------------------------------------------|
| bool | True if harvest should be done, false if not |

#### **`harvest`**	

Harvests the Strategy, recognizing any profits or losses and adjusting the Strategy's position.
In rare cases the Strategy is in emergency shutdown, this will exit the Strategy's position.
This may only be called by governance, the strategist, or the keeper.

```
function harvest() external override onlyKeepers
```

**Events emitted:**
- Harvested(want_profit, want_loss, want_debtPayment, debtOutstanding)

#### **`withdraw`**	

Withdraws _amountNeeded (represented in wrapped tokens) to specific vault. This may only be called by the Vault.

```
function withdraw(uint256 _amountNeeded) external override returns (uint256 _loss)
```

**Parameters:**

| Name          | Type    | Description                          |
|---------------|---------|--------------------------------------|
| _amountNeeded | uint256 | Amount to withdraw of wrapped tokens |

**Return value:**

| Name  | Type    | Description                        |
|-------|---------|------------------------------------|
| _loss | uint256 | Any losses produced by withdrawing |

#### **`sweep`**	

Removes tokens from this Strategy that are not the type of tokens managed by this Strategy. This may be used in case of accidentally sending the wrong kind of token to this Strategy. Tokens will be sent to governance. This will fail if an attempt is made to sweep `want`, or any tokens that are protected by this Strategy. This may only be called by governance.

```
function sweep(address _token) external override onlyGovernance
```

**Parameters:**

| Name   | Type    | Description                                           |
|--------|---------|-------------------------------------------------------|
| _token | address | Address of token that should be removed from strategy |
