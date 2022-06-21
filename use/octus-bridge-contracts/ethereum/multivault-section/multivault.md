# MultiVault

#### **`deposit`**	

Transfer tokens to the Everscale.  
Works both for native and alien tokens. Approve is required only for alien tokens deposit.

```
function deposit(
        EverscaleAddress memory recipient,
        address token,
        uint amount
    ) external override nonReentrant
        tokenNotBlacklisted(token)
        initializeToken(token) onlyEmergencyDisabled
```

**Parameters:**

| Name      | Type                    | Description                  |
|-----------|-------------------------|------------------------------|
| recipient | EverscaleAddress memory | Everscale recipient          |
| token     | address                 | EVM token address            |
| amount    | uint                    | Amount of tokens to transfer |

**Events emitted:**
- Deposit

#### **`saveWithdrawNative`**

Saves withdrawal for native token (does the necessary checks regarding token and chain, calculates fees and mints).

```
function saveWithdrawNative(
        bytes memory payload,
        bytes[] memory signatures
    ) external override nonReentrant
        withdrawalNotSeenBefore(payload) onlyEmergencyDisabled
```

**Parameters:**

| Name       | Type           | Description        |
|------------|----------------|--------------------|
| payload    | bytes memory   | Withdraw payload   |
| signatures | bytes[] memory | List of signatures |

**Events emitted:**
- Withdraw

#### **`saveWithdrawAlien`**

Saves withdrawal for alien token (does the necessary checks regarding token and chain, calculates fees and mints).

```
function saveWithdrawAlien(
        bytes memory payload,
        bytes[] memory signatures
    )
        external
        override
        nonReentrant
        withdrawalNotSeenBefore(payload)
        onlyEmergencyDisabled
```

**Parameters:**

| Name       | Type           | Description                                          |
|------------|----------------|------------------------------------------------------|
| payload    | bytes memory   | Withdraw payload (later processed to EverscaleEvent) |
| signatures | bytes[] memory | List of signatures                                   |

**Events emitted:**
- Withdraw

#### **`skim`**

Skim (removes) multivault fees for specific token.
If `skim_to_everscale` is true, than fees will be sent to Everscale.
Otherwise, tokens will be transferred to the `governance` address.

```
function skim(
        address token,
        bool skim_to_everscale
    ) external override nonReentrant onlyGovernanceOrManagement
```

**Parameters:**

| Name              | Type    | Description                                  |
|-------------------|---------|----------------------------------------------|
| token             | address | Token address, can be both native or alien   |
| skim_to_everscale | bool    | Are skim fees applicable on Everscale or not |

**Events emitted:**
- SkimFee

#### **`migrateAlienTokenToVault`**

Transfers specified token to specified vault.

```
function migrateAlienTokenToVault(
        address token,
        address vault
    ) external override onlyGovernance
```

**Parameters:**

| Name  | Type    | Description                                |
|-------|---------|--------------------------------------------|
| token | address | Address of alien token                     |
| vault | address | Vault address where to migrate alien token |

**Events emitted:**
- TokenMigrated

#### **`calculateMovementFee`**
	
Calculates fee for deposit or withdrawal.

```
function calculateMovementFee(
        uint256 amount,
        address _token,
        Fee fee
    ) public view returns (uint256)
```

**Parameters:**

| Name   | Type    | Description                          |
|--------|---------|--------------------------------------|
| amount | uint256 | Amount of tokens to deposit/withdraw |
| _token | address | Token address                        |
| fee    | Fee     | Fee type (Deposit=0, Withdraw=1)     |

**Return value:**

| Type    | Description                |
|---------|----------------------------|
| uint256 | Fee for deposit/withdrawal |

#### **`_activateToken`**

Activates specified token with all the information about it.

```
function _activateToken(
        address token,
        bool isNative
    ) internal
```

**Parameters:**

| Name     | Type    | Description                   |
|----------|---------|-------------------------------|
| token    | address | Token address                 |
| isNative | bool    | True if native, false if not  |

**Events emitted:**
- TokenActivated

#### **`_transferToEverscaleNative`**

Emits NativeTransfer event to signify native token transfer to Everscale network.

```
function _transferToEverscaleNative(
        address _token,
        EverscaleAddress memory recipient,
        uint amount
    ) internal
```

**Parameters:**

| Name      | Type                    | Description                  |
|-----------|-------------------------|------------------------------|
| _token    | address                 | Native token address         |
| recipient | EverscaleAddress memory | Everscale recipient data     |
| amount    | uint                    | Amount of tokens to transfer |

**Events emitted:**
- NativeTransfer

#### **`_transferToEverscaleAlien`**

Emits AlienTransfer event to signify alien token transfer to Everscale network.

```
function _transferToEverscaleAlien(
        address _token,
        EverscaleAddress memory recipient,
        uint amount
    ) internal
```

**Parameters:**

| Name      | Type                    | Description                  |
|-----------|-------------------------|------------------------------|
| _token    | address                 | Alien token address          |
| recipient | EverscaleAddress memory | Everscale recipient data     |
| amount    | uint                    | Amount of tokens to transfer |

**Events emitted:**
- AlienTransfer

#### **`_getNativeWithdrawalToken`**

Gets the native token based on provided parameters, deploys and activates it if it isn't already active.

```
function _getNativeWithdrawalToken(
        NativeWithdrawalParams memory withdrawal
    ) internal returns (address token)
```

**Parameters:**

| Name       | Type                          | Description                                                    |
|------------|-------------------------------|----------------------------------------------------------------|
| withdrawal | NativeWithdrawalParams memory | Native withdrawal token data (includes workchain id, address…) |

#### **`_deployTokenForNative`**	

Deploys token as native.

```
function _deployTokenForNative(
        EverscaleAddress memory native,
        TokenMeta memory meta
    ) internal returns (address token)
```

**Parameters:**

| Name   | Type                    | Description                       |
|--------|-------------------------|-----------------------------------|
| native | EverscaleAddress memory | Everscale address data            |
| meta   | TokenMeta memory        | Meta data of token to be deployed |

**Return value:**

| Name  | Type    | Description               |
|-------|---------|---------------------------|
| token | address | Address of deployed token |

**Events emitted:**
- TokenCreated

#### **`_processWithdrawEvent`**

Process' withdraw event by verifying signatures and decoding the event and checking the event configuration.

```
function _processWithdrawEvent(
        bytes memory payload,
        bytes[] memory signatures,
        EverscaleAddress memory configuration
    ) internal view returns (EverscaleEvent memory)
```

**Parameters:**

| Name          | Type                    | Description                                        |
|---------------|-------------------------|----------------------------------------------------|
| payload       | bytes memory            | EverscaleEvent data encoded to bytes               |
| signatures    | bytes[] memory          | List of signatures                                 |
| configuration | EverscaleAddress memory | Everscale address data needed for required checks  |

**Return value:**

| Type           | Description                 |
|----------------|-----------------------------|
| EverscaleEvent | New withdraw EverscaleEvent |
