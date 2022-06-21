# Bridge

#### **`verifySignedEverscaleEvent`**
	
Verifying signatures from EverscaleEvent (is there enough signatures, is the round rotten, etc.)

```
function verifySignedEverscaleEvent(bytes memory payload, bytes[] memory signatures) override public view returns (uint32 errorCode)
```

**Parameters:**

| Name       | Type           | Description                               |
|------------|----------------|-------------------------------------------|
| payload    | bytes memory   | EverscaleEvent structure encoded to bytes |
| signatures | bytes[] memory | Payload signatures                        |

**Return value:**

| Name      | Type   | Description |
|-----------|--------|-------------|
| errorCode | uint32 | Error code  |

#### **`recoverSignature`**

Recover signer from the payload and signature.

```
function recoverSignature(bytes memory payload, bytes memory signature) public pure returns (address signer)
```

**Parameters:**

| Name      | Type         | Description             |
|-----------|--------------|-------------------------|
| payload   | bytes memory | Signer encoded to bytes |
| signature | bytes memory | Signature in bytes      |

**Return value:**

| Name   | Type    | Description                 |
|--------|---------|-----------------------------|
| signer | address | Decoded signature’s address |

#### **`forceRoundRelays`**

Forced set of next round relayers.
Can be called only by `roundSubmitter`.

```
function forceRoundRelays(uint160[] calldata _relays, uint32 roundEnd) override external
```

**Parameters:**

| Name     | Type               | Description          |
|----------|--------------------|----------------------|
| _relays  | uint160[] calldata | Next round relayers  |
| roundEnd | uint32             | End of the round     |

#### **`setRoundSubmitter`**

Set round submitter.
Can be called only by owner.

```
function setRoundSubmitter(address _roundSubmitter) override external onlyOwner
```

**Parameters:**

| Name            | Type    | Description                   |
|-----------------|---------|-------------------------------|
| _roundSubmitter | address | New round submitter’s address |

**Events emitted:**
- UpdateRoundSubmitter

#### **`setRoundRelays`**	

Grant relayer permission for set of addresses at specific round.

```
function setRoundRelays(bytes calldata payload, bytes[] calldata signatures) override external notCached(payload)
```

**Parameters:**

| Name       | Type             | Description                               |
|------------|------------------|-------------------------------------------|
| payload    | bytes calldata   | EverscaleEvent structure encoded to bytes |
| signatures | bytes[] calldata | Signatures encoded to bytes               |

#### **`decodeRoundRelaysEventData`**	

Decodes payload event data for round relayers.

```
function decodeRoundRelaysEventData(bytes memory payload) public pure returns (uint32 round, uint160[] memory _relays, uint32 roundEnd)
```

**Parameters:**

| Name    | Type         | Description                                                 |
|---------|--------------|-------------------------------------------------------------|
| payload | bytes memory | Round relayers event data (EverscaleEvent) encoded to bytes |

**Return value:**

| Name     | Type             | Description                |
|----------|------------------|----------------------------|
| round    | uint32           | Round id                   |
| _relays  | uint160[] memory | Addresses of the relayers  |
| roundEnd | uint32           | End of round               |

#### **`decodeEverscaleEvent`**	

Decodes payload data for everscale event.

```
function decodeEverscaleEvent(bytes memory payload) external pure returns
```

**Parameters:**

| Name    | Type         | Description                               |
|---------|--------------|-------------------------------------------|
| payload | bytes memory | EverscaleEvent structure encoded to bytes |

#### **`banRelays`**	

Puts specified relayer addresses on a blacklist.

```
function banRelays(address[] calldata _relays) override external onlyOwner
```

**Parameters:**

| Name    | Type               | Description                |
|---------|--------------------|----------------------------|
| _relays | address[] calldata | Addresses of the relayers  |

**Events emitted:**
- BanRelay

#### **`unbanRelays`**

Takes out specified relayer addresses from a blacklist.

```
function unbanRelays(address[] calldata _relays) override external onlyOwner
```

**Parameters:**

| Name    | Type               | Description                |
|---------|--------------------|----------------------------|
| _relays | address[] calldata | Addresses of the relayers  |

**Events emitted:**
- BanRelay

#### **`_setRound`**	

Creates a new round and makes a map including all rounds and relayers.

```
function _setRound(uint32 round, uint160[] memory _relays, uint32 roundEnd) internal
```

**Parameters:**

| Name     | Type              | Description            |
|----------|-------------------|------------------------|
| round    | uint32            | Round Id               |
| _relays  | uint160[] memory  | Addresses of relayers  |
| roundEnd | uint32            | End of the round       |

**Events emitted:**
- NewRound
- RoundRelay

#### **`_countRelaySignatures`**	

Counts all the valid relayers signatures.

```
function _countRelaySignatures(bytes memory payload, bytes[] memory signatures, uint32 round) internal view returns (uint32)
```

**Parameters:**

| Name       | Type           | Description                          |
|------------|----------------|--------------------------------------|
| payload    | bytes memory   | EverscaleEvent data encoded to bytes |
| signatures | bytes[] memory | List of signatures                   |
| round      | uint32         | Round Id                             |

**Return value:**

| Type   | Description                   |
|--------|-------------------------------|
| uint32 | Number of relayers signatures |