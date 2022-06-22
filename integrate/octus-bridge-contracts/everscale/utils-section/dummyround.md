# DummyRound

#### **`addRelays`**

Adds the number of new relayers as provided in method parameter.

```
function addRelays(uint count) external
```

**Parameters:**

| Name  | Type | Description                   |
|-------|------|-------------------------------|
| count | uint | Number of new relayers to add |

#### **`relayKeys`**

Gets the public keys of all the relayers.

```
function relayKeys() public view responsible returns (uint256[])
```

**Return value:**

| Type      | Description                  |
|-----------|------------------------------|
| uint256[] | Public keys of the relayers  |
