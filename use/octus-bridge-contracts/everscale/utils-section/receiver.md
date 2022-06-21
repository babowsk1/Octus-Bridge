# Receiver

#### **`fetchRelays`**

Fetches relayers for specified round.

```
function fetchRelays(address roundContract) public
```

**Parameters:**

| Name          | Type    | Description                       |
|---------------|---------|-----------------------------------|
| roundContract | address | The address of the round contract |

#### **`receiveRoundRelays`**	

Receives the list of keys which represent the round relayers.

```
function receiveRoundRelays(uint[] keys) public
```

**Parameters:**

| Name | Type   | Description                    |
|------|--------|--------------------------------|
| keys | uint[] | Public keys of round relayers  |