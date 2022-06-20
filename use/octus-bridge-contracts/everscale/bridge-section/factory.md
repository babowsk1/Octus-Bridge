# Factory

### EthereumEventConfigurationFactory

#### **`deploy`**
	
Creates new contract instance of EthereumEventConfiguration.

```
function deploy(
        address _owner,
        IEthereumEventConfiguration.BasicConfiguration basicConfiguration,
        IEthereumEventConfiguration.EthereumEventConfiguration networkConfiguration
    ) external view reserveMinBalance(MIN_CONTRACT_BALANCE)
```

**Parameters:**

| Name                 | Type                       | Description                                                                                                 |
|----------------------|----------------------------|-------------------------------------------------------------------------------------------------------------|
| _owner               | address                    | The address of the event configuration owner                                                                |
| basicConfiguration   | BasicConfiguration         | Basic configuration for event including the event code, event initial balance etc.                          |
| networkConfiguration | EthereumEventConfiguration | The configuration of the ethereum event, including event emitter, chain id, start and end block number etc. |

#### **`deriveConfigurationAddress`**

Initializes state by setting contract, base and network configurations and config code and returns configuration address based on the state initialized.

```
function deriveConfigurationAddress(
        IEthereumEventConfiguration.BasicConfiguration basicConfiguration,
        IEthereumEventConfiguration.EthereumEventConfiguration networkConfiguration
    ) external view returns(address)
```

**Parameters:**

| Name                 | Type                       | Description                                                                                                 |
|----------------------|----------------------------|-------------------------------------------------------------------------------------------------------------|
| basicConfiguration   | BasicConfiguration         | Basic configuration for event including the event code, event initial balance etc.                          |
| networkConfiguration | EthereumEventConfiguration | The configuration of the ethereum event, including event emitter, chain id, start and end block number etc. |
| networkConfiguration | EthereumEventConfiguration | The configuration of the ethereum event, including event emitter, chain id, start and end block number etc. |

**Return values:**

| Type    | Description               |
|---------|---------------------------|
| address | The configuration address |

### EverscaleEventConfigurationFactory

#### **`deploy`**

Creates new contract instance of EverscaleEventConfiguration.

function deploy(
        address _owner,
        IEverscaleEventConfiguration.BasicConfiguration basicConfiguration,
        IEverscaleEventConfiguration.EverscaleEventConfiguration networkConfiguration
    ) external view reserveMinBalance(MIN_CONTRACT_BALANCE)

**Parameters:**

| Name                 | Type                        | Description                                                                                        |
|----------------------|-----------------------------|----------------------------------------------------------------------------------------------------|
| _owner               | address                     | The address of the event configuration owner                                                       |
| basicConfiguration   | BasicConfiguration          | Basic configuration for event including the event code, event initial balance etc.                 |
| networkConfiguration | EverscaleEventConfiguration | The configuration of the everscale event, including event emitter, start and end block number etc. |

#### **`deriveConfigurationAddress`**

Initializes state by setting contract, base and network configurations and config code and returns configuration address based on the state initialized.

```
function deriveConfigurationAddress(
        IEverscaleEventConfiguration.BasicConfiguration basicConfiguration,
        IEverscaleEventConfiguration.EverscaleEventConfiguration networkConfiguration
    ) external view returns(address)
```

**Parameters:**

| Name                 | Type                        | Description                                                                                        |
|----------------------|-----------------------------|----------------------------------------------------------------------------------------------------|
| basicConfiguration   | BasicConfiguration          | Basic configuration for event including the event code, event initial balance etc.                 |
| networkConfiguration | EverscaleEventConfiguration | The configuration of the everscale event, including event emitter, start and end block number etc. |

**Return values:**

| Type    | Description               |
|---------|---------------------------|
| address | The configuration address |

### ProxyTokenTransferFactory

#### **`deploy`**

Creates new contract instance of ProxyTokenTransfer.

```
function deploy(address _owner, uint _randomNonce) external reserveMinBalance(MIN_CONTRACT_BALANCE)
```

**Parameters:**

| Name         | Type    | Description                                |
|--------------|---------|--------------------------------------------|
| _owner       | address | The address of the deployed contract owner |
| _randomNonce | uint    | Value used for building the initial state  |

#### **`deriveProxyAddress`**

Initializes state by setting contract, variables and proxy code and returns proxy address based on the state initialized.

```
function deriveProxyAddress(
        uint _randomNonce
    ) external view returns(address)
```

**Parameters:**

| Name         | Type  | Description                                |
|--------------|-------|--------------------------------------------|
| _randomNonce | uint  | Value used for building the initial state  |

**Return values:**

| Type         | Description                               |
|--------------|-------------------------------------------|
| address      | Proxy address used for token transfer     |


