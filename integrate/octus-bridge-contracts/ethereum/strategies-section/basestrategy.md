# BaseStrategy

#### **`harvestTrigger`**	

Provides a signal to the keeper that harvest() should be called. The keeper will provide the estimated gas cost that they would pay to call harvest() and this function should use that estimate to make a determination if calling it is "worth it" for the keeper.

```
function harvestTrigger(uint256 callCost) public virtual view returns (bool)
```

**Parameters:**

| Name     | Type    | Description                          |
|----------|---------|--------------------------------------|
| callCost | uint256 | Amount of cost for calling harvest() |

**Return value:**

| Type | Description                                            |
|------|--------------------------------------------------------|
| bool | True if harvest() should be called, false if otherwise |

#### **`harvest`**	

Harvests the Strategy, recognizing any profits or losses and adjusting the Strategy's position.

```
function harvest() external virtual onlyKeepers
```

**Events emitted:**
- Harvested(profit, loss, debtPayment, debtOutstanding)

#### **`withdraw`**

Withdraws _amountNeeded to vault

```
function withdraw(uint256 _amountNeeded) external virtual returns (uint256 _loss)
```

**Parameters:**

| Name          | Type    | Description                  |
|---------------|---------|------------------------------|
| _amountNeeded | uint256 | Amount of tokens to withdraw |

**Return value:**

| Name  | Type    | Description                                 |
|-------|---------|---------------------------------------------|
| _loss | uint256 | Any losses created while liquidating tokens |

#### **`prepareMigration`**

Do anything necessary to prepare this Strategy for migration, such as transferring any reserve or LP tokens, CDPs, or other tokens or stores of value.

```
function prepareMigration(address _newStrategy) internal virtual
```

**Parameters:**

| Name         | Type    | Description                  |
|--------------|---------|------------------------------|
| _newStrategy | address | New strategy’s vault address |

#### **`migrate`**

Transfers all want tokens from this strategy to a new strategy. Can only be called by the governance or the vault.

```
function migrate(address _newStrategy) external
```

**Parameters:**

| Name         | Type    | Description                  |
|--------------|---------|------------------------------|
| _newStrategy | address | New strategy’s vault address |

#### **`sweep`**	

Removes tokens from this Strategy that are not the type of tokens managed by this Strategy.

```
function sweep(address _token) external virtual onlyGovernance
```

**Parameters:**

| Name   | Type    | Description                                               |
|--------|---------|-----------------------------------------------------------|
| _token | address | Address of token to transfer out of this strategy’s vault |

**Events emitted:**
- `IERC20Upgradeable(_token).safeTransfer(governance()`, `IERC20Upgradeable(_token).balanceOf(address(this)))`
