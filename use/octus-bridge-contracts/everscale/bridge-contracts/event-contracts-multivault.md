# event-contracts/multivault

### MultiVaultEverscaleEventAlien

#### **`afterSignatureCheck`**

Returns DAO event in slice format.

```
function afterSignatureCheck(TvmSlice body, TvmCell /*message*/) private inline view returns (TvmSlice)
```

**Parameters:**

| Name | Type     | Description                      |
|------|----------|----------------------------------|
| body | TvmSlice | Contains data such as functionId |
|      | TvmCell  |                                  |

**Return values:**

| Type     | Description                           |
|----------|---------------------------------------|
| TvmSlice | DAO event represented in slice format |

#### **`close`**

When event is confirmed/rejected transfer back gas used for triggering event.

```
function close() external view
```

#### **`onInit`**

Initialize alien token. 

```
function onInit() override internal
```

#### **`receiveTokenMeta`**

Receives meta token.

```
function receiveTokenMeta(
        uint256 base_chainId_,
        uint160 base_token_,
        string name,
        string symbol,
        uint8 decimals
    ) external override
```

**Parameters:**

| Name          | Type    | Description          |
|---------------|---------|----------------------|
| base_chainId_ | uint256 | EVM network chain ID |
| base_token_   | uint160 | EVM token address    |
| name          | string  | Token name           |
| symbol        | string  | Token symbol         |
| decimals      | uint8   | Token decimals       |

#### **`receiveAlienTokenRoot`**

Sets token root and loads relayers.

```
function receiveAlienTokenRoot(
        address token_
    ) external override
```

**Parameters:**

| Name   | Type     | Description                               |
|--------|----------|-------------------------------------------|
| token_ | address  | The address of the alien token to receive |

#### **`onRelaysLoaded`**

Updates event data and does the change for status.

```
function onRelaysLoaded() override internal
```

### MultiVaultEverscaleEventNative

#### **`afterSignatureCheck`**	

Returns DAO event info in slice format.

```
function afterSignatureCheck(TvmSlice body, TvmCell /*message*/) private inline view returns (TvmSlice)
```

**Parameters:**

| Name | Type     | Description                      |
|------|----------|----------------------------------|
| body | TvmSlice | Contains data such as functionId |
|      | TvmCell  |                                  |

**Return values:**

| Type     | Description                           |
|----------|---------------------------------------|
| TvmSlice | DAO event represented in slice format |

#### **`close`**

When event is confirmed/rejected transfer back gas used for triggering event.

```
function close() external view
```

#### **`onInit`**

Initializes native token.

```
function onInit() override internal
```

#### **`receiveProxyTokenWallet`**

Sets token wallet address and loads relayers.

```
function receiveProxyTokenWallet(address tokenWallet_) external override
```

**Parameters:**

| Name         | Type    | Description                     |
|--------------|---------|---------------------------------|
| tokenWallet_ | address | The address of the token wallet |

#### **`onRelaysLoaded`**

Updates event data and does the change for status.

```
function onRelaysLoaded() override internal
```

### MultiVaultEVMEventAlien

#### **`afterSignatureCheck`**

Returns DAO event info in slice format.

```
function afterSignatureCheck(
        TvmSlice body,
        TvmCell
    ) private inline view returns (TvmSlice)
```

**Parameters:**

| Name | Type     | Description                      |
|------|----------|----------------------------------|
| body | TvmSlice | Contains data such as functionId |
|      | TvmCell  |                                  |

**Return values:**

| Type     | Description                           |
|----------|---------------------------------------|
| TvmSlice | DAO event represented in slice format |

#### **`onInit`**

Initializes evm alien token by decoding event data, sets recipient address and gets details about ethereum event configuration.

```
function onInit() override internal
```

#### **`receiveConfigurationDetails`**

Gets configuration details based on proxy about alien token root.

```
function receiveConfigurationDetails(
        IEthereumEventConfiguration.BasicConfiguration,
        IEthereumEventConfiguration.EthereumEventConfiguration _networkConfiguration,
        TvmCell
    ) external override
```

**Parameters:**

| Name                  | Type                       | Description                                                                                                 |
|-----------------------|----------------------------|-------------------------------------------------------------------------------------------------------------|
|                       | BasicConfiguration         | Basic configuration for event including the event code, event initial balance etc.                          |
| _networkConfiguration | EthereumEventConfiguration | The configuration of the ethereum event, including event emitter, chain id, start and end block number etc. |
|                       | TvmCell                    |                                                                                                             |

#### **`receiveAlienTokenRoot`**

Sets token root based on token_ param and loads relayers.

```
function receiveAlienTokenRoot(address token_) external override
```

**Return values:**

| Name   | Type    | Description                               |
|--------|---------|-------------------------------------------|
| token_ | address | The address of the alien token to receive |

#### **`onConfirm`**

Encodes token root, amount and recipient's address to cell format and confirms event.

```
function onConfirm() internal override
```

### MultiVaultEVMEventNative

#### **`afterSignatureCheck`**

Returns DAO event info in slice format.

```
function afterSignatureCheck(TvmSlice body, TvmCell /*message*/) private inline view returns (TvmSlice)
```

**Parameters:**

| Name | Type     | Description                      |
|------|----------|----------------------------------|
| body | TvmSlice | Contains data such as functionId |
|      | TvmCell  |                                  |

**Return values:**

| Type     | Description                           |
|----------|---------------------------------------|
| TvmSlice | DAO event represented in slice format |

#### **`onInit`**

Initializes native token event and gets details about event configuration.

```
function onInit() override internal
```

#### **`receiveConfigurationDetails`**

Retrieves wallet based on proxy.

```
function receiveConfigurationDetails(
        IEthereumEventConfiguration.BasicConfiguration,
        IEthereumEventConfiguration.EthereumEventConfiguration _networkConfiguration,
        TvmCell
    ) external override
```

**Parameters:**

| Name                  | Type                       | Description                                                                                                 |
|-----------------------|----------------------------|-------------------------------------------------------------------------------------------------------------|
|                       | BasicConfiguration         | Basic configuration for event including the event code, event initial balance etc.                          |
| _networkConfiguration | EthereumEventConfiguration | The configuration of the ethereum event, including event emitter, chain id, start and end block number etc. |
|                       | TvmCell                    |                                                                                                             |

#### **`receiveProxyTokenWallet`**

Sets token wallet address and loads relayers.

```
function receiveProxyTokenWallet(address tokenWallet_) external override
```

**Parameters:**

| Name         | Type    | Description                     |
|--------------|---------|---------------------------------|
| tokenWallet_ | address | The address of the token wallet |

#### **`onConfirm`**

Encodes token wallet, amount and recipient's address to cell format and confirms event.

```
function onConfirm() internal override
```
