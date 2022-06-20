# event-contracts/staking

### StakingEthEvent

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

#### **`onConfirm`**

Confirms an event.

```
function onConfirm() override internal
```

#### **`onReject`**

Transfers gas to the initializer after rejection.

```
function onReject() override internal
```

### StakingTonEvent	

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
