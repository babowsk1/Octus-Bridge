# event-contracts/base

### **BaseEvent**

#### **`onRelaysLoaded`**

Changes status to Pending

```
function onRelaysLoaded() virtual internal
```

#### **`loadRelays`**

Gets address of the current relayer round

```
function loadRelays() internal view
```

#### **`_checkVoteReceiver`**

Checks if vote receiver is this address

```
function _checkVoteReceiver(address voteReceiver)
```

**Parameters:**

| Name         | Type    | Description                         |
|--------------|---------|-------------------------------------|
| voteReceiver | address | Address of the receiver of the vote |

#### **`receiveRoundAddress`**	

Based on the round contract retrieves round address 

```
function receiveRoundAddress(
        address roundContract,
        uint32 roundNum
    ) external onlyStaking
```

**Parameters:**

| Name          | Type    | Description                       |
|---------------|---------|-----------------------------------|
| roundContract | address | The address of the round contract |
| roundNum      | uint32  | The round’s number                |

#### **`receiveRoundRelays`**

Loads relayers based on their keys

```
function receiveRoundRelays(uint[] keys) external onlyRelayRound
```

**Parameters:**

| Name | Type   | Description                  |
|------|--------|------------------------------|
| keys | uint[] | Keys of the round’s relayers |

### **EthereumBaseEvent**

#### **`confirm`**	

Confirm event. Can be called only by relayer which is in charge at this round. Can be called only when event configuration is in Pending status

```
function confirm(address voteReceiver) public eventPending
```

**Parameters:**

| Name         | Type    | Description                                                  |
|--------------|---------|--------------------------------------------------------------|
| signature    | bytes   | relayer's signature of the Everscale event data              |
| voteReceiver | address | Address of the receiver of the vote (event contract address) |

**Events emitted:**
- Confirm

#### **`reject`**

Reject event. Can be called only by relayer which is in charge at this round.  
Can be called only when event configuration is in Pending status.

```
function reject(address voteReceiver) public eventPending
```

**Parameters:**

| Name         | Type    | Description                                                  |
|--------------|---------|--------------------------------------------------------------|
| voteReceiver | address | Address of the receiver of the vote (event contract address) |

**Events emitted:**
- Reject

