# Registry

#### **`newVaultRelease`**	

Checks the id of vault release and the api versions, after which adds the vault to all the vault releases.

```
function newVaultRelease(address vault) external onlyOwner
```

**Parameters:**

| Name  | Type    | Description                     |
|-------|---------|---------------------------------|
| vault | address | Address of a new vault released |

**Events emitted:**
- NewVaultRelease

#### **`_newProxyVault`**

Checks the vault release target, deploys vault release proxy (owned by proxy admin) and initializes vault.

```
function _newProxyVault(address token, address governance, uint256 targetDecimals, uint256 vault_release_target) internal returns (address)
```

**Parameters:**

| Name                 | Type    | Description                                |
|----------------------|---------|--------------------------------------------|
| token                | address | Token address of a new vault               |
| governance           | address | Governance address                         |
| targetDecimals       | uint256 | Target decimals for a new vault            |
| vault_release_target | uint256 | Target address for deploying vault’s proxy |

**Return value:**

| Type    | Description           |
|---------|-----------------------|
| address | Vault’s proxy address |

#### **`_registerVault`**	

Checks the vault id and the api version, after which adds new vault and its token to all the vaults and registers the token if not already registered.

```
function _registerVault(address token, address vault) internal
```

**Parameters:**

| Name  | Type    | Description                |
|-------|---------|----------------------------|
| token | address | Token address of the vault |
| vault | address | Vault’s address            |

**Events emitted:**
- NewVault

#### **`newVault`**

Creates new proxy vault with all the necessary data and registers that new vault and its token.

```
function newVault(address token, uint256 targetDecimals, uint256 vaultReleaseDelta) external onlyOwner returns (address)
```

**Parameters:**

| Name              | Type    | Description                                     |
|-------------------|---------|-------------------------------------------------|
| token             | address | Token address of the new vault                  |
| targetDecimals    | uint256 | Target decimals value                           |
| vaultReleaseDelta | uint256 | Value used for calculating vault release target |

**Return value:**

| Type    | Description         |
|---------|---------------------|
| address | New vault’s address |

#### **`newExperimentalVault`**	

Creates new proxy vault with all the necessary data.

```
function newExperimentalVault(address token, address governance, uint256 targetDecimals, uint256 vaultReleaseDelta) external returns (address)
```

**Parameters:**

| Name              | Type    | Description                                     |
|-------------------|---------|-------------------------------------------------|
| token             | address | Token’s address of the vault                    |
| governance        | address | Vault’s governance address                      |
| targetDecimals    | uint256 | Target decimals value                           |
| vaultReleaseDelta | uint256 | Value used for calculating vault release target |

**Return value:**

| Type    | Description               |
|---------|---------------------------|
| address | New proxy vault’s address |

**Events emitted:**
- NewExperimentalVault 

#### **`endorseVault`**

Checks the vault governance and vault api version, after which it registers the vault.

```
function endorseVault(address vault, uint256 vaultReleaseDelta) external onlyOwner
```

**Parameters:**

| Name              | Type    | Description                                     |
|-------------------|---------|-------------------------------------------------|
| vault             | address | Vault’s address                                 |
| vaultReleaseDelta | address | Value used for calculating vault release target |

#### **`tagVault`**	

Adds tag to specified vault.

```
function tagVault(address vault, string memory tag) external
```

**Parameters:**

| Name  | Type          | Description     |
|-------|---------------|-----------------|
| vault | address       | Vault’s address |
| tag   | "string" memory | Vault’s tag     |

**Events emitted:**
- VaultTagged
