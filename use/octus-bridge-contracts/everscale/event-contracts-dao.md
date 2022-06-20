# event-contracts/dao

### DaoEthereumActionEvent

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
function close() public view
```

#### **`getGasBackAddress`**

Returns address which will receive returned gas.

```
function getGasBackAddress() private view returns(address)
```

**Return values:**

| Type    | Description                         | Description                      |
|---------|-------------------------------------|----------------------------------|
| address | Address to return the remaining gas | Contains data such as functionId |

#### **`getDecodedData`**

Decodes DAO event data from ethereum and returns address for returned gas, chain ID and actions done in ETH.

```
function getDecodedData() public view responsible returns (
        address gasBackAddress,
        uint32 chainId,
        ActionStructure.EthActionStripped[] actions)
```

**Return values:**

| Name           | Type                | Description                         |
|----------------|---------------------|-------------------------------------|
| gasBackAddress | address             | Address to return the remaining gas |
| chainId        | uint32              | The id of the chain                 |
| actions        | EthActionStripped[] | The array of ethereum actions       |


