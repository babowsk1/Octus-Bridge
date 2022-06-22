# MultiVaultToken

#### **`_transfer`**	

 Moves `amount` of tokens from `sender` to `recipient`.

```
function transfer(address to, uint256 amount) public virtual override returns (bool)
```

**Parameters:**

| Name   | Type    | Description                  |
|--------|---------|------------------------------|
| to     | address | Recipient’s address          |
| amount | uint256 | Amount of tokens to transfer |

Return value:

| Type | Description                                  |
|------|----------------------------------------------|
| bool | True if transfer is successful, false if not |

**Events emitted:**
- Transfer

#### **`_mint`**

Creates `amount` tokens and assigns them to `account`, increasing the total supply

```
function _mint(address account, uint256 amount) internal virtual
```

**Parameters:**

| Name    | Type    | Description                                           |
|---------|---------|-------------------------------------------------------|
| account | address | Address of the account where to assign created tokens |
| amount  | uint256 | Amount of tokens to be created                        |

**Events emitted:**
- Transfer

#### **`_burn`**

Destroys `amount` tokens from `account`, reducing the total supply.

```
function _burn(address account, uint256 amount) internal virtual
```

**Parameters:**

| Name    | Type    | Description                                         |
|---------|---------|-----------------------------------------------------|
| account | address | Account address in which tokens should be destroyed |
| amount  | uint256 | Amount of tokens to be destroyed                    |

**Events emitted:**
- Transfer

#### **`_approve`**

Sets `amount` as the allowance of `spender` over the `owner` s tokens.

```
function _approve(
        address owner,
        address spender,
        uint256 amount
    ) internal virtual
```

**Parameters:**
| Name    | Type    | Description                                     |
|---------|---------|-------------------------------------------------|
| owner   | address | Address of the owner whose tokens will be spent |
| spender | address | Address of the owner’s tokens spender           |
| amount  | uint256 | Allowed amount of tokens which spender can use  |

**Events emitted:**
- Approval

#### **`_spendAllowance`**

Updates `owner` s allowance for `spender` based on spent `amount`.

```
function _spendAllowance(
        address owner,
        address spender,
        uint256 amount
    ) internal virtual
```

**Parameters:**

| Name    | Type    | Description                                     |
|---------|---------|-------------------------------------------------|
| owner   | address | Address of the owner whose tokens will be spent |
| spender | address | Address of the owner’s tokens spender           |
| amount  | uint256 | Allowed amount of tokens which spender can use  |