# RelayRound

#### **`hasUnclaimedReward`**

Checks if user has unclaimed rewards. 

```
function hasUnclaimedReward(address _relay_staker_addr) external view responsible returns (bool has_reward)
```

**Parameters:**

| Name               | Type    | Description       |
|--------------------|---------|-------------------|
| _relay_staker_addr | address | Address of staker |

**Return value:**

| Name       | Type | Description                                    |
|------------|------|------------------------------------------------|
| has_reward | bool | True if it has unclaimed rewards, false if not |

#### **`getRewardForRound`**

Calculates reward for certain round and sends it to user.

```
function getRelayByStakerAddress(
        address _relay_staker_addr
    ) external view responsible returns (uint256 _ton_key, uint160 _eth_addr, address _staker_addr, uint128 _staked_tokens)
```

**Parameters:**

| Name               | Type    | Description    |
|--------------------|---------|----------------|
| _relay_staker_addr | address | Staker address |

**Return value:**

| Name           | Type    | Description                |
|----------------|---------|----------------------------|
| _ton_key       | uint256 | Ton account’s public key   |
| _eth_addr      | uint160 | Ethereum account’s address |
| _staker_addr   | address | Staker address             |
| _staked_tokens | uint128 | Amount of tokens staked    |

#### **`sendRelaysToRelayRound`**

Sets relayers to the specific round.

```
function sendRelaysToRelayRound(address relay_round_addr, uint32 count) external override onlyRoot
```

**Parameters:**

| Name             | Type    | Description                                 |
|------------------|---------|---------------------------------------------|
| relay_round_addr | address | Address of relayer round                    |
| count            | uint32  | Number of relayers to send to relayer round |

#### **`_checkRelaysInstalled`**

Checks whether there are enough relayers installed.

```
function _checkRelaysInstalled() internal
```

#### **`destroy`**

Destroy round if ended.

```
function destroy() external override onlyRoot
```

#### **`onCodeUpgrade`**

Sets relayer round data based on the upgraded data.

```
function onCodeUpgrade(TvmCell upgrade_data) private
```

**Parameters:**

| Name         | Type    | Description                                 |
|--------------|---------|---------------------------------------------|
| upgrade_data | TvmCell | Upgraded election data in cell format       |
| count        | uint32  | Number of relayers to send to relayer round |

#### **`upgrade`**	

Upgrades relayer round data and code.

```
function upgrade(TvmCell code, uint32 new_version, address send_gas_to) external onlyRoot
```

**Parameters:**

| Name        | Type    | Description                             |
|-------------|---------|-----------------------------------------|
| code        | TvmCell | relayer round’s platform code           |
| new_version | uint32  | New version of relayer round’s platform |
| send_gas_to | address | Address where to send remaining gas     |

**Events emitted:**
- RelayRoundCodeUpgraded
