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

