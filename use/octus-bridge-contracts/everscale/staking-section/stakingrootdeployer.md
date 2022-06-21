# StakingRootDeployer

#### **`deploy`**	

Creates and deploys new staking root.

```
function deploy(
        address _admin,
        address _dao_root,
        address _rewarder,
        address _rescuer,
        address _bridge_event_config_eth_ton,
        address _bridge_event_config_ton_eth,
        address _tokenRoot,
        uint32 _deploy_nonce
    ) public returns(address)
```

**Parameters:**

| Name                         | Type    | Description                                                         |
|------------------------------|---------|---------------------------------------------------------------------|
| _admin                       | address | Address of staking root’s admin                                     |
| _dao_root                    | address | DAO root’s address                                                  |
| _rewarder                    | address | Rewarder address                                                    |
| _rescuer                     | address | Rescuer address                                                     |
| _bridge_event_config_eth_ton | address | Address of the bridge event configuration handling ethereum to ton  |
| _bridge_event_config_ton_eth | address | Address of the bridge event configuration handling ton to ethereum  |
| _tokenRoot                   | address | Staking token root’s address                                        |
| _deploy_nonce                | uint32  | Flag used for deploying new Staking contract                        |

**Return value:**

| Type    | Description                          |
|---------|--------------------------------------|
| address | Address of the deployed staking root |
