# Convex3crv

#### **`_approveBasic`**	

Sets unlimited access for curve and booster to the wrapped token and IERC20 tokens. 

```
function _approveBasic() internal override
```

#### **`_approveDex`**	

Sets unlimited access for dex to curve and convex tokens.

```
function _approveDex() internal override
```

#### **`calc_wrapped_from_want`**	

Calculates amount of want tokens after wrapping.

```
function calc_wrapped_from_want(uint256 want_amount) public view override returns (uint256)
```

**Parameters:**

| Name        | Type    | Description            |
|-------------|---------|------------------------|
| want_amount | uint256 | Amount of want tokens  |

**Return value:**

| Type    | Description                                |
|---------|--------------------------------------------|
| uint256 | Amount of wrapped tokens after calculation |

#### **`wrap`**	

Wraps tokens and adds them to Curve. 

```
function wrap(uint256 want_amount) internal override returns (uint256 expected_return)
```

**Parameters:**

| Name        | Type    | Description           |
|-------------|---------|-----------------------|
| want_amount | uint256 | Amount of want tokens |

**Return value:**

| Name            | Type    | Description                     |
|-----------------|---------|---------------------------------|
| expected_return | uint256 | Amount of tokens after wrapping |

#### **`prepareReturn`**	

Checks whether convex and curve token amount is greater than 0, if so in dex swaps exact tokens of crv and cvx to tokens, checks whether dai, usdt and usdc amount is greater than 0, if yes, adds liquidity to curve's pool. Calculates profit, loss and debtPayment amount and returns them.

```
function prepareReturn(uint256 _debtOutstanding) internal override returns(uint256 _profit, uint256 _loss, uint256 _debtPayment)
```

**Parameters:**

| Name             | Type    | Description |
|------------------|---------|-------------|
| _debtOutstanding | uint256 | Debt value  |

**Return value:**

| Name         | Type    | Description                |
|--------------|---------|----------------------------|
| _profit      | uint256 | Amount of profit made      |
| _loss        | uint256 | Amount of loss             |
| _debtPayment | uint256 | Amount of debt to be payed |