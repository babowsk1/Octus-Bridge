# DAO

#### **`decodeEthActionsEventData`**	

Decodes the payload into the everscale event data format.

```
function decodeEthActionsEventData(bytes memory payload) public pure returns(int8 _wid, uint256 _addr, uint32 chainId, EthAction[] memory actions)
```

**Parameters:**

| Name    | Type         | Description                          |
|---------|--------------|--------------------------------------|
| payload | bytes memory | EverscaleEvent data encoded to bytes |

**Return value:**

| Name    | Type               | Description              |
|---------|--------------------|--------------------------|
| _wid    | int8               | Workchain Id             |
| _addr   | uint256            | Address                  |
| chainId | uint32             | Chain Id                 |
| actions | EthAction[] memory | List of Ethereum actions |

#### **`execute`**	

Executes a set of ETH actions gotten after decoding the payload and verifying signatures.

```
function execute(bytes calldata payload, bytes[] calldata signatures) override external nonReentrant notCached(payload) returns (bytes[] memory responses)
```

**Parameters:**

| Name       | Type             | Description                                 |
|------------|------------------|---------------------------------------------|
| payload    | bytes calldata   | Encoded EverscaleEvent with payload details |
| signatures | bytes[] calldata | Payload signatures                          |

**Return value:**

| Name      | Type           | Description                            |
|-----------|----------------|----------------------------------------|
| responses | bytes[] memory | Bytes-encoded payload action responses |
