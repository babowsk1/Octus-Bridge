# ConvexAIEth

#### **`calc_wrapped_from_want`**

Calculates amount of want tokens after wrapping.

```
function calc_wrapped_from_want(uint256 want_amount) public view override returns (uint256)
```

**Parameters:**

| Name        | Type    | Description           |
|-------------|---------|-----------------------|
| want_amount | uint256 | Amount of want tokens |

**Return value:**

| Type    | Description                                |
|---------|--------------------------------------------|
| uint256 | Amount of wrapped tokens after calculation |

#### **`unwrap`**	

If wrapped amount is greater than 0, remove wrapped amount from curve's liquidity and deposit balance of the contract to the wrapped ethereum.

```
function unwrap(uint256 wrapped_amount) internal override returns (uint256 result_val)
```

**Parameters:**

| Name           | Type    | Description                        |
|----------------|---------|------------------------------------|
| wrapped_amount | uint256 | Amount of wrapped tokens to unwrap |

**Return value:**

| Name       | Type    | Description                       |
|------------|---------|-----------------------------------|
| result_val | uint256 | Amount of tokens after unwrapping |

#### **`wrap`**	

Calculates wrapped amount from want amount, removes wrapped tokens from wrapped ethereum and after converting them, deposits them to the curve's pool.

```
function wrap(uint256 want_amount) internal override returns (uint256 expected_return)
```

**Parameters:**

| Name        | Type    | Description                   |
|-------------|---------|-------------------------------|
| want_amount | uint256 | Amount of want tokens to wrap |

**Return value:**

| Name             | Type    | Description                     |
|------------------|---------|---------------------------------|
| expected_return  | uint256 | Amount of tokens after wrapping |

#### **`prepareReturn`**	

Calculates curve and convex tokens and swaps them to ETH, sells extra rewards, after that is done, calculates and returns value of profit, loss and dept payment.

```
function prepareReturn(uint256 _debtOutstanding) internal override returns (uint256 _profit, uint256 _loss, uint256 _debtPayment)
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
