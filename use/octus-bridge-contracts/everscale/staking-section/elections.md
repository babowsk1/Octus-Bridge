# Elections

#### **`applyForMembership`**
	
Adds new relayer to the list of request nodes and accepts request.

```
function applyForMembership(
        address staker_addr,
        uint256 ton_pubkey,
        uint160 eth_addr,
        uint128 tokens,
        uint32 lock_time,
        uint32 code_version
    ) external override onlyUserData(staker_addr)
```

**Parameters:**

| Name         | Type    | Description                    |
|--------------|---------|--------------------------------|
| staker_addr  | address | Address of the staker applying |
| ton_pubkey   | uint256 | Public key of ton account      |
| eth_addr     | uint160 | Address of ethereum account    |
| tokens       | uint128 | Number of staker’s tokens      |
| lock_time    | uint32  | Duration of locking the tokens |
| code_version | uint32  | Code version                   |

#### **`destroy`**	

Should be called after transfer of relayer data to next relayer round.

```
function destroy() external override onlyRoot
```

#### **`finish`**	

Ends election if not yet ended and sends gas back to root.

```
function finish(uint32 code_version) external override onlyRoot
```

**Parameters:**

| Name         | Type   | Description             |
|--------------|--------|-------------------------|
| code_version | uint32 | Election’s version code |

#### **`sendRelaysToRelayRound`**	

Sets relayers to the relayer round.

```
function sendRelaysToRelayRound(address relay_round_addr, uint32 relays_count) external override onlyRoot
```

**Parameters:**

| Name             | Type    | Description                     |
|------------------|---------|---------------------------------|
| relay_round_addr | address | Address of the relayer round    |
| relays_count     | uint32  | Number of relayers in the round |

#### **`upgrade`**	

Upgrades election data and sets new code.

```
function upgrade(TvmCell code, uint32 new_version, address send_gas_to) external onlyRoot
```

**Parameters:**

| Name        | Type    | Description                         |
|-------------|---------|-------------------------------------|
| code        | TvmCell | Election’s platform code            |
| new_version | uint32  | New version of election’s platform  |
| sendGasTo   | address | Address where to send remaining gas |

**Events emitted:**
- ElectionCodeUpgraded

#### **`onCodeUpgrade`**	

Takes current version info and creates origin node after contract initialization.

```
function onCodeUpgrade(TvmCell upgrade_data) private
```

**Parameters:**

| Name         | Type    | Description                           |
|--------------|---------|---------------------------------------|
| upgrade_data | TvmCell | Upgraded election data in cell format |


#### **`_buildUserDataParams`**	

Builds user data params.

```
function _buildUserDataParams(address user) private view returns (TvmCell)
```

**Parameters:**

| Name | Type    | Description       |
|------|---------|-------------------|
| user | address | User data address |

**Return value:**

| Type    | Description                     |
|---------|---------------------------------|
| TvmCell | User Data params in cell format |

#### **`_buildPlatformInitData`**	

Sets initial platform data.

```
function _buildPlatformInitData(address platform_root, uint8 platform_type, TvmCell initial_data) private view returns (TvmCell)
```

**Parameters:**

| Name          | Type    | Description                          |
|---------------|---------|--------------------------------------|
| platform_root | address | Address of the platform              |
| platform_type | uint8   | Type of the platform                 |
| initial_data  | TvmCell | Initial platform data in cell format |

**Return value:**

| Type    | Description                           |
|---------|---------------------------------------|
| TvmCell | Platform initial state in cell format |
