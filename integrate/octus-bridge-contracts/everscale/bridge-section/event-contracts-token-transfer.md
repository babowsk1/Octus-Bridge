# event-contracts/token-transfer

### TokenTransferEthereumEvent

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

Notifies change of event status and loads relayers.

```
function onInit() override internal
```

#### **`onConfirm`**

Confirms an event and notifies change of event status.

```
function onConfirm() override internal
```

#### **`onReject`**

Notifies change of event status and transfers all gas to the initializer

```
function onReject() override internal
```

#### *`notifyEventStatusChanged`**

Notify the owner contract that the event contract status has been changed. Used to easily collect all confirmed events by the user's wallet.

```
function notifyEventStatusChanged() internal view
```

### TokenTransferEverscaleEvent

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

Finishes token transfer and sends remaining gas to the owner

```
function close() public view
```

#### **`onInit`**

Notifies change of event status and loads relayers  

```
function onInit() override internal
```

#### **`onConfirm`**

Notifies change of event status

```
function onConfirm() override internal
```

#### **`onReject`**

Notifies change of event status 

```
function onReject() override internal
```

#### **`notifyEventStatusChanged`**

Notify the owner contract that the event contract status has been changed. Used to easily collect all confirmed events by the user's wallet.

```
function notifyEventStatusChanged() internal view
```
