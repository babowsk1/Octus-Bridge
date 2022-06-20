# Bridge 

#### **`deriveConnectorAddress`**

Derive connector address by it's id.

```
function deriveConnectorAddress(
        uint64 id
    ) override external returns(address connector)
```

**Parameters:**

| Name         | Type    | Description  |
|--------------|---------|--------------|
| id           | uint 64 | Connector id |

**Return values:**

| Name      | Type    | Description                  |
|-----------|---------|------------------------------|
| connector | address | The address of the connector |

#### **`_deriveConnectorAddress`**	

Initializes state by setting contract, id, bridge address and connector code and returns connector address based on the state initialized

```
function _deriveConnectorAddress(
        uint64 id
    ) internal view returns (address)
```

**Parameters:**

| Name | Type   | Description  |
|------|--------|--------------|
| id   | uint64 | Connector id |

**Return values:**

| Type    | Description                  |
|---------|------------------------------|
| address | The address of the connector |

#### **`deployConnector`**

Deploy new connector.

```
function deployConnector(
        address _eventConfiguration
    ) override public reserveMinBalance(MIN_CONTRACT_BALANCE)
```

**Parameters:**

| Name                | Type     | Description                            |
|---------------------|----------|----------------------------------------|
| _eventConfiguration | address  | Event configuration address to connect |

**Events emitted:**
- ConnectorDeployed
