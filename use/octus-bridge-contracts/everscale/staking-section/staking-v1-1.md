# StakingV1_1

#### **`upgrade`**	

Upgrades all codes and main data related to staking version v1.1.

```
function upgrade(TvmCell code, address send_gas_to) external onlyAdmin
```

**Parameters:**

| Name        | Type    | Description                         |
|-------------|---------|-------------------------------------|
| code        | TvmCell | Staking V1_1 platform’s code        |
| send_gas_to | address | Address where to send remaining gas |

#### **`sendRelaysToRelayRound`**	

Sets relayers to the specific round.

```
function sendRelaysToRelayRound(
        uint32 relay_round,
        uint256[] _ton_keys,
        uint160[] _eth_addrs,
        address[] _staker_addrs,
        uint128[] _staked_tokens
    ) external onlyAdmin
```

**Parameters:**

| Name           | Type      | Description                          |
|----------------|-----------|--------------------------------------|
| relay_round    | uint32    | relayer round id                     |
| _ton_keys      | uint256[] | List of ton accounts’ public keys    |
| _eth_addrs     | uint160[] | List of ethereum accounts’ addresses |
| _staker_addrs  | address[] | List of stakers’ address             |
| _staked_tokens | uint128[] | List of amounts of staked tokens     |


#### **`onCodeUpgrade`**

After the code upgrade, this method emits the StakingUpdated event.

```
function onCodeUpgrade(TvmCell upgrade_data) private
```

**Parameters:**

| Name         | Type    | Description                           |
|--------------|---------|---------------------------------------|
| upgrade_data | TvmCell | Upgraded election data in cell format |

**Events emitted:**
- StakingUpdated

