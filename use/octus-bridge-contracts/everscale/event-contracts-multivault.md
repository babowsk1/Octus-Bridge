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

| Type     | Description                           | Description                      |
|----------|---------------------------------------|----------------------------------|
| TvmSlice | DAO event represented in slice format | Contains data such as functionId |

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

| Type     | Description                           | Description                      |
|----------|---------------------------------------|----------------------------------|
| TvmSlice | DAO event represented in slice format | Contains data such as functionId |

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
