# event-configuration-contracts

### **EthereumEventConfiguration**

#### **`buildEventInitData`**

Build initial data for the event contract by extending the event vote data with configuration params.

```
function buildEventInitData(
        IEthereumEvent.EthereumEventVoteData eventVoteData
    ) internal view returns(
        IEthereumEvent.EthereumEventInitData eventInitData)
```

**Parameters:**

****

| Name          | Type                  | Description                                  |
| ------------- | --------------------- | -------------------------------------------- |
| eventVoteData | EthereumEventVoteData | Event vote data structure, passed by relayer |
| signatures    | bytes\[] memory       | Payload signatures                           |

#### **`deployEvent`**

Deploys the event contract (creates a new instance of EthereumBaseEvent contract).

```
function deployEvent(
        IEthereumEvent.EthereumEventVoteData eventVoteData
    ) external override reserveMinBalance(MIN_CONTRACT_BALANCE)
```

**Parameters**

| Name          | Type                  | Description               |
|---------------|-----------------------|---------------------------|
| eventVoteData | EthereumEventVoteData | Event vote data structure |

**Events emitted:**
- NewEventContract

#### **`deriveEventAddress`**

Derive the Ethereum event contract address from its init data.

```
function deriveEventAddress(
        IEthereumEvent.EthereumEventVoteData eventVoteData
    ) override public view responsible
    returns(address eventContract)
```

**Parameters:**

| Type    | Description                         |
|---------|-------------------------------------|
| address | Address to return the remaining gas |

### EverscaleEventConfiguration

#### **`buildEventInitData`**

Extends event vote data with configuration params.

```
function buildEventInitData(
        IEverscaleEvent.EverscaleEventVoteData eventVoteData
    ) internal view returns(
        IEverscaleEvent.EverscaleEventInitData eventInitData)
```

**Parameters:**

| Name          | Type                   | Description                                  |
|---------------|------------------------|----------------------------------------------|
| eventVoteData | EverscaleEventVoteData | Event vote data structure, passed by relayer |

**Return values:**

| Name          | Type                   | Description                     |
|---------------|------------------------|---------------------------------|
| eventInitData | EverscaleEventVoteData | Initial data for event contract |

#### **`deployEvent`**

Deploy event contract (creates new instance of EverscaleBaseEvent contract).

```
function deployEvent(
        IEverscaleEvent.EverscaleEventVoteData eventVoteData
    ) override external reserveMinBalance(MIN_CONTRACT_BALANCE)
```

**Parameters:**

| Name          | Type                   | Description               |
|---------------|------------------------|---------------------------|
| eventVoteData | EverscaleEventVoteData | Event vote data structure |

**Events emitted:**
- NewEventContract

#### **`deriveEventAddress`**	

Derives the Everscale event contract address from it's initial data.

```
function deriveEventAddress(
        IEverscaleEvent.EverscaleEventVoteData eventVoteData
    ) override public view responsible
    returns (address eventContract)
```

**Parameters:**

| Name          | Type                   | Description               |
|---------------|------------------------|---------------------------|
| eventVoteData | EverscaleEventVoteData | Event vote data structure |

**Return values:**

| Name          | Type    | Description                                           |
|---------------|---------|-------------------------------------------------------|
| eventContract | address | Address of the corresponding everscale event contract |

#### **`onEventConfirmedExtended`**

Receives "confirm" callback from the event contract and checks event contract correctness. If it's correct, then sends the callback to the proxy with the same signature.

```
function onEventConfirmedExtended(
        IEthereumEvent.EthereumEventInitData eventInitData,
        TvmCell _meta,
        address gasBackAddress
    ) external override reserveMinBalance(MIN_CONTRACT_BALANCE)
```

**Parameters:**

| Type    | Description                         |
|---------|-------------------------------------|
| address | Address to return the remaining gas |

