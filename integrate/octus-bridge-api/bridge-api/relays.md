# Relays

{% swagger method="post" path="/relay_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get relayer" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "frozenStake": "258917.752572214000",
  "untilFrozen": 1661463628000,
  "latestReward": "0",
  "totalReward": "8800.73179149",
  "successfulRounds": 18,
  "totalCountRounds": 20,
  "relayTotalConfirmed": 7291,
  "potentialTotalConfirmed": 8403,
  "evmStats": [
    {
      "chainId": 1,
      "relayConfirmed": 1801,
      "potentialConfirmed": 2047
    },
    ...
    {
      "chainId": 43114,
      "relayConfirmed": 106,
      "potentialConfirmed": 123
    }
  ]
} 
```
{% endswagger-response %}
{% endswagger %}

This function is used to return information about a specific relayer based on its address.

It can be used anywhere where details about a specific relayer is needed such as details about events and their confirmation, validating rounds, rewards, stake etc.

### Request parameters

Required body parameters:

| Name         | Example value                                                      | Comment                        |
| ------------ | ------------------------------------------------------------------ | ------------------------------ |
| relayAddress | 0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557 | Address of the desired relayer |

### Response fields explanation

| Name                    | Example value       | Comment                                                |
| ----------------------- | ------------------- | ------------------------------------------------------ |
| evmStats                | -                   | List of data related to the evm actions                |
| chainId                 | 1                   | Id of the chain                                        |
| potentialConfirmed      | 2047                | Number of potential events confirmed                   |
| relayConfirmed          | 1801                | Actual number of events confirmed                      |
| frozenStake             | 258917.752572214000 | Frozen stake of the relayer                            |
| latestReward            | 0                   | Reward acquired from the last round                    |
| potentialTotalConfirmed | 20                  | Total number of potential events confirmed             |
| relayTotalConfirmed     | 7291                | Actual total number of confirmed events                |
| successfulRounds        | 18                  | Rounds that ended successfully for the certain relayer |
| totalCountRounds        | 20                  | Total number of rounds relayer participated in         |
| totalReward             | 8800.73179149       | Total amount of reward the relayer acquired            |
| untilFrozen             | 1661463628000       | Date time until the stake will be frozen               |

### Example

```javascript
app.post('/relays_pages/relay_info', (req, res) => {
    axios({
        method: 'post',
        url: `${apiUrl}/relays_pages/relay_info`,
        data: {
            relayAddress: req.body.relayAddress
        }
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
})​
```

{% swagger method="post" path="/relay_round_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get relayer round info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "relayAddress": "0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557",
  "roundNum": 15,
  "stake": "258917.752572214000",
  "eventsConfirmed": 661,
  "tonToEthUsdt": "5567068.9741",
  "ethToTonUsdt": "6119978.1405",
  "relayPlace": 1,
  "eventsConfirmedShare": "0.9511",
  "totalRoundConfirms": 695,
  "roundAddress": "0:20e866e80bb8ded0ad14f7317a58b05d378fd108306aafed64650465cd68b19e",
  "startTime": 1653999926000,
  "endTime": 1654604726000,
  "evmStats": [
   {
   ...
  {
      "chainId": 250,
      "relayConfirmed": 7,
      "potentialConfirmed": 7
    },
    {
      "chainId": 43114,
      "relayConfirmed": 16,
      "potentialConfirmed": 17
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

This function use to get validation round info.

It can be used for showing a relayer’s efforts in one specific round.\
Following data about the relayer’s performance based on the round number can be displayed:\
How much a relayer staked to become a relayer, number of events he confirmed, volume from all the transfers relayer validated happened from everscale to ethereum network and vice versa shown in USDTs, round address, start and end time of the round.

### Request parameters:

Required body parameters:

| Name         | Example value                                                      | Comment                        |
| ------------ | ------------------------------------------------------------------ | ------------------------------ |
| relayAddress | 0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557 | Address of the desired relayer |

### Response fields explanation:

| Name                 | Example value                                                      | Comment                                                                             |
| -------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| endTime              | 1654604726000                                                      | Date time of the validation round’s end                                             |
| ethToTonUsdt         | 6119978.1405                                                       | Total amount of ethereum tokens in USDT swapped to everscale tokens and transferred |
| eventsConfirmed      | 661                                                                | Total number of events the relayer confirmed in the current round                   |
| evmStats             | : \[                                                               | List of data related to the evm events                                              |
| chainId              | 1                                                                  | Id of the chain                                                                     |
| potentialConfirmed   | 144                                                                | Number of potential events confirmed                                                |
| relayConfirmed       | 143                                                                | Number of actual events confirmed                                                   |
| relayAddress         | 0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557 | Address of the relayer                                                              |
| relayPlace           | 1                                                                  | Place of the relayer                                                                |
| roundAddress         | 0:20e866e80bb8ded0ad14f7317a58b05d378fd108306aafed64650465cd68b19e | Address of the round certain relayer is participating in                            |
| roundNum             | 15                                                                 | Round number                                                                        |
| stake                | 258917.752572214000                                                | Amount relayer staked to become one of the participants                             |
| startTime            | 1653999926000                                                      | Date time of round start                                                            |
| tonToEthUsdt         | 5567068.9741                                                       | Total amount of everscale tokens in USDT swapped to ethereum tokens and transferred |
| totalRoundConfirms   | 695                                                                | Number of total confirms in the monitored round                                     |
| eventsConfirmedShare | 0.9511                                                             | Share of the relayer per event confirmed                                            |

### Example

```java
app.post('/relays_pages/relay_round_info', (req, res) => {
    axios({
        method: 'post',
        url: `${apiUrl}/relays_pages/relay_round_info`,
        data: {
            relayAddress: req.body.relayAddress,
            roundNum: req.body.roundNum
        }
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
})
```

{% swagger method="post" path="/relays_round_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get relayers round info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "relays": [
    {
      "relayAddress": "0:ef79b4aac06c33ab3435943d196de9ba9ee48a3e4572c86a8ad3a2bf84b4f767",
      "roundNum": 15,
      "stake": "100000",
      "eventsConfirmed": 661,
      "tonToEthUsdt": "5567068.9741",
      "ethToTonUsdt": "6485680.9782",
      "relayPlace": null,
      "eventsConfirmedShare": "0.9511",
      "totalRoundConfirms": 695,
      "roundAddress": "0:20e866e80bb8ded0ad14f7317a58b05d378fd108306aafed64650465cd68b19e",
      "startTime": 1653999926000,
      "endTime": 1654604726000,
      "evmStats": []
    },
    ...
   {
      "relayAddress": "0:a2848bfafd47a43ac029e3c55c7241804be7fe3331ed3e965862431a78f528e1",
      "roundNum": 15,
      "stake": "100000",
      "eventsConfirmed": 630,
      "tonToEthUsdt": "5567068.9741",
      "ethToTonUsdt": "5732605.3024",
      "relayPlace": null,
      "eventsConfirmedShare": "0.9065",
      "totalRoundConfirms": 695,
      "roundAddress": "0:20e866e80bb8ded0ad14f7317a58b05d378fd108306aafed64650465cd68b19e",
      "startTime": 1653999926000,
      "endTime": 1654604726000,
      "evmStats": []
    }
  ],
  "totalCount": 23
}
```
{% endswagger-response %}
{% endswagger %}

This function returns list of relayers and details about them based on the round number they are part of.&#x20;

Can be used for listing all or certain number of relayers when it comes to one validation round. \
Some of the details about the relayers are number of confirmed events and the share per event, relay’s address, list of events, place of a relayer and also info about the round such as start and end time, round number and address, etc.

### Request parameters

Required body parameters:

| Name     | Example value  | Comment                                                                                            |
| -------- | -------------- | -------------------------------------------------------------------------------------------------- |
| limit    | 10             | Maximum number of relayers to be retrieved                                                         |
| offset   | 0              | Offset                                                                                             |
| ordering | stakeascending | Value based on which the retrieved relayer data will be ordered (stakeascending, stakedescending…) |
| roundNum | 15             | Round number                                                                                       |

### Response fields explanation



| Name                 | Example value                                                      | Comment                                                                                                   |
| -------------------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| relays               | : \[                                                               | List of relays participating in the given round, determined by the amount set in the limit body parameter |
| endTime              | 1654604726000                                                      | Date time of the validation round’s end                                                                   |
| ethToTonUsdt         | 5567068.9741                                                       | Total amount of ethereum tokens in USDT swapped to everscale tokens and transferred                       |
| eventsConfirmed      | 661                                                                | Total number of events the relayer confirmed in the current round                                         |
| eventsConfirmedShare | 0.9511                                                             | Share of the relayer per event confirmed                                                                  |
| evmStats             | : \[]                                                              | List of data related to the evm events                                                                    |
| chainId              | 0                                                                  | Id of the chain                                                                                           |
| potentialConfirmed   | 0                                                                  | Number of potential events confirmed                                                                      |
| relayConfirmed       | 0                                                                  | Number of actual events confirmed                                                                         |
| relayAddress         | 0:ef79b4aac06c33ab3435943d196de9ba9ee48a3e4572c86a8ad3a2bf84b4f767 | Address of the relayer                                                                                    |
| relayPlace           | null                                                               | Place of the relayer                                                                                      |
| roundAddress         | 0:20e866e80bb8ded0ad14f7317a58b05d378fd108306aafed64650465cd68b19e | Address of the round certain relayer is participating in                                                  |
| roundNum             | 15                                                                 | Round number                                                                                              |
| stake                | 100000                                                             | Amount relayer staked to become one of the participants                                                   |
| startTime            | 1653999926000                                                      | Date time of round start                                                                                  |
| tonToEthUsdt         | 5567068.9741                                                       | Total amount of everscale tokens in USDT swapped to ethereum tokens and transferred                       |
| totalRoundConfirms   | 695                                                                | Number of total confirms in the monitored round                                                           |
| totalCount           | 23                                                                 | Total number of relayers participating in the round with given round number                               |

### Example

```java
app.post('/relays_pages/relays_round_info', (req, res) => {
    axios({
        method: 'post',
        url: `${apiUrl}/relays_pages/relays_round_info`,
        data: {
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            roundNum: req.body.roundNum
        }
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
})
```

{% swagger method="post" path="/all_relay_ronds_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get all validation rounds info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful resonse" %}
```
{
  "relays": [
    {
      "relayAddress": "0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557",
      "roundNum": 1,
      "stake": "244636",
      "eventsConfirmed": 97,
      "tonToEthUsdt": "573326.1229",
      "ethToTonUsdt": "401075.7860",
      "relayPlace": null,
      "eventsConfirmedShare": "0.8981",
      "totalRoundConfirms": 108,
      "roundAddress": "0:77f4e7eb93d7fb3432f297782f2cd2e5fb2a62bb05d8a9590ea54c6ab954254d",
      "startTime": 1645303857000,
      "endTime": 1645908657000,
      "evmStats": []
    },
    ...
   {
      "relayAddress": "0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557",
      "roundNum": 10,
      "stake": "244636",
      "eventsConfirmed": 529,
      "tonToEthUsdt": "5204152.7479",
      "ethToTonUsdt": "4509235.2178",
      "relayPlace": null,
      "eventsConfirmedShare": "0.8773",
      "totalRoundConfirms": 603,
      "roundAddress": "0:cc312267aa40b7f9a56ce1aad46dbca5088c2d30ee1ba88555d2e97941ac9816",
      "startTime": 1650975926000,
      "endTime": 1651580726000,
      "evmStats": []
    }
  ],
  "totalCount": 18
}
```
{% endswagger-response %}
{% endswagger %}

This function returns all validation relay rounds in which specified relayer took part in.&#x20;

It can be used for monitoring a relayer's activity and history by retrieving data such as details about events and share per event, round details, relayer’s place and stake, etc. only by inputting relayer’s address.

### Request parameters

Required body parameters:

| Name        | Example value                                                      | Comment                                                                                            |
| ----------- | ------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| limit       | 10                                                                 | Maximum number of relayers to be retrieved                                                         |
| offset      | 0                                                                  | Offset                                                                                             |
| ordering    | roundnumascending                                                  | Value based on which the retrieved relayer data will be ordered (stakeascending, stakedescending…) |
| userAddress | 0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557 | Address of the relayer                                                                             |

### Response fields explanation&#x20;

| Name               | Example value                                                      | Comment                                                                             |
| ------------------ | ------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| evmStats           | \[]                                                                | List of data related to the evm events                                              |
| chainId            | 0                                                                  | Id of the chain                                                                     |
| potentialConfirmed | 0                                                                  | Number of potential events confirmed                                                |
| relayConfirmed     | 0                                                                  | Number of actual events confirmed                                                   |
| relayAddress       | 0:aacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557  | Address of the relayer                                                              |
| relayPlace         | null                                                               | Place of the relayer                                                                |
| roundAddress       | 0:77f4e7eb93d7fb3432f297782f2cd2e5fb2a62bb05d8a9590ea54c6ab954254d | Address of the round certain relayer is participating in                            |
| roundNum           | 1                                                                  | Round number                                                                        |
| stake              | 244636                                                             | Amount relayer staked to become one of the participants                             |
| startTime          | 1645303857000                                                      | Date time of round start                                                            |
| tonToEthUsdt       | 573326.1229                                                        | Total amount of everscale tokens in USDT swapped to ethereum tokens and transferred |
| totalRoundConfirms | 108                                                                | Number of total confirms in the monitored round                                     |
| totalCount         | 18                                                                 | Number of validation rounds in which the desired relayer takes part                 |

### Example

```graphql
app.post('/relays_pages/all_relay_rounds_info', (req, res) => {
    axios({
        method: 'post',
        url: `${apiUrl}/relays_pages/all_relay_rounds_info`,
        data: {
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            userAddress: req.body.userAddress
        }
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
})
```

{% swagger method="post" path="/round_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get validation round info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "roundNum": 10,
  "totalStake": "2549112.692146446000",
  "totalStakeChange": "8.5100",
  "averageRelayStake": "106213.02883900",
  "averageRelayStakeChange": "-0.5300",
  "eventsConfirmed": 603,
  "relaysCount": 24,
  "relaysCountChange": "9.0900",
  "tonToEthUsdt": "6007826.4910",
  "ethToTonUsdt": "5204152.7479",
  "evmStats": [
    {
      "chainId": 1,
      "relayConfirmed": 0,
      "potentialConfirmed": 142
    },
    ...
     {
      "chainId": 43114,
      "relayConfirmed": 0,
      "potentialConfirmed": 7
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

This function returns basic information about relayers based on their addresses, round number and stake.

It can be used for filtering rounds based on their number and showing information about them such as stake and stake changes, information about events, relayers and change in number of them, amount of USDTs transferred through the round duration.

### Request parameters

Required body parameters:

| Name     | Example value | Comment      |
| -------- | ------------- | ------------ |
| roundNum | 10            | Round number |

### Response fields explanation



| Name                    | Example value        | Comment                                                                             |
| ----------------------- | -------------------- | ----------------------------------------------------------------------------------- |
| averageRelayStake       | 106213.02883900      | Average relayers stake                                                              |
| averageRelayStakeChange | -0.5300              | Change of the average relayers stake in percentage                                  |
| ethToTonUsdt            | 5204152.7479         | Total amount of ethereum tokens in USDT swapped to everscale tokens and transferred |
| eventsConfirmed         | 603                  | Total number of events the relayer confirmed in the current round                   |
| evmStats                | : \[                 | List of data related to the evm events                                              |
| chainId                 | 1                    | Id of the chain                                                                     |
| potentialConfirmed      | 142                  | Number of potential events confirmed                                                |
| relayConfirmed          | 0                    | Number of actual events confirmed                                                   |
| relaysCount             | 24                   | Total number of relayers in the desired round                                       |
| relaysCountChange       | 9.0900               | Change of number of relayers participating in the round in percentage               |
| roundNum                | 10                   | Round number                                                                        |
| tonToEthUsdt            | 6007826.4910         | Total amount of everscale tokens in USDT swapped to ethereum tokens and transferred |
| totalStake              | 2549112.692146446000 | Sum of all the stakes relayers invested in the round                                |
| totalStakeChange        | 8.5100               | Change of total stake invested in percentage                                        |

### Example

```java
app.post('/relays_pages/round_info', (req, res) => {
    axios({
        method: 'post',
        url: `${apiUrl}/relays_pages/round_info`,
        data: {
            roundNum: req.body.roundNum
        }
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })

})​
```

{% swagger method="post" path="/search/relays" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get relayers info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful response" %}
```
{
  "relays": [
    {
      "relayAddress": "0:099341ccbe3f2db59432fc1cc794773b9da06048d14e43ae24ae224dd768145d",
      "stake": "100000",
      "slashed": false,
      "currentRound": true,
      "successfulRounds": 10,
      "totalRounds": 10,
      "createdAt": 1651074897000,
      "relayTotalConfirmed": 4053,
      "potentialTotalConfirmed": 4746
    },
  ...
  {
      "relayAddress": "0:92beea3fa73ba9fa2420442eb89c7c16fdb899e9d4c10f84e34f13f651beb25f",
      "stake": "100000",
      "slashed": false,
      "currentRound": true,
      "successfulRounds": 20,
      "totalRounds": 20,
      "createdAt": 1645013257000,
      "relayTotalConfirmed": 7894,
      "potentialTotalConfirmed": 8924
    }
  ],
  "totalCount": 27
}
```
{% endswagger-response %}
{% endswagger %}

This function **** returns basic information about relayers based on their addresses, round number and stake.

### Request parameters

Required body parameters:

| Name                    | Example value                                                      | Comment                                                                                           |
| ----------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------- |
| createdAtGe             | 0                                                                  | Value representing bottom border of the date time relayer was created                             |
| createdAtLe             | 0                                                                  | Value representing top border of the date time relayer was created                                |
| limit                   | 10                                                                 | Maximum number of relayers to be retrieved                                                        |
| offset                  | 0                                                                  | Offset                                                                                            |
| ordering                | stakeascending                                                     | Value based on which the retrieved relayer data will be ordered (stakeascending, stakedescending) |
| relayAddresses          | 0:79fc8ce8d32211a4c49adf7de1c9c0fa682ff3a13124ff027f6b92faa308ffeb | List of relayers (addresses)                                                                      |
| roundNum                | 10                                                                 | Round number                                                                                      |
| stakeGe                 | 50                                                                 | Bottom border of the stake amount relayer invested for participating in the round                 |
| stakeLe                 | 1000000                                                            | Top border of the stake amount relayer invested for participating in the round                    |
| transferContractAddress | 0:cbd090198d22e4b1a77227ba2bff58a05a32049ef2908aebfb461cacd6a474c8 | Address of the transfer contract                                                                  |

Parameters used for the test:

| Name     | Value          |
| -------- | -------------- |
| limit    | 10             |
| offset   | 0              |
| ordering | stakeascending |

### Response fields explanation



### Example&#x20;

```java
app.post('/relays_pages/search/relays', (req, res) => {
    axios({
        method: 'post',
        url: `${apiUrl}/relays_pages/search/relays`,
        data: {
            createdAtGe: req.body.createdAtGe,
            createdAtLe: req.body.createdAtLe,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            relayAddresses: req.body.relayAddresses,
            roundNum: req.body.roundNum,
            stakeGe: req.body.stakeGe,
            stakeLe: req.body.stakeLe,
            transferContractAddress: req.body.transferContractAddress
        }
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
})
```

{% swagger method="post" path="/search/relays_events" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get relayer's events" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "relays": [
    {
      "transferKind": "ethtoton",
      "contractAddress": "0:91b879d842d2292db57abd10d1cd6e83959dd27fb70189d02032314c0de542a9",
      "chainId": 1,
      "tokenAddress": "0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2",
      "from": "0xcbefe3344284444ac8141c930207b8ff82a3177e",
      "to": "0:1fcdda0bdb6cc28476575f1617949188fb9f29d35b9f86217438baf3519058c3",
      "amount": "90000",
      "timestamp": 1655983612000
    },
    ...
     {
      "transferKind": "ethtoton",
      "contractAddress": "0:91b879d842d2292db57abd10d1cd6e83959dd27fb70189d02032314c0de542a9",
      "chainId": 1,
      "tokenAddress": "0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2",
      "from": "0xcbefe3344284444ac8141c930207b8ff82a3177e",
      "to": "0:1fcdda0bdb6cc28476575f1617949188fb9f29d35b9f86217438baf3519058c3",
      "amount": "90000",
      "timestamp": 1655983612000
    }
  ],
  "totalCount": 18
}
```
{% endswagger-response %}
{% endswagger %}

This function returns details about relayer’s events based on the chain id of the event, kind of transfer, receiver’s address, sender’s address, token address, relayer’s address, contract’s address, round number.

It can be used for filtering all the events based on the required parameters and displaying them in the list form along with information such as amount transferred, chain id, sender’s address, receiver’s address, token address etc.

### Request parameters

Required body parameters:

| Name                    | Example value                                                      | Comment                                                         |
| ----------------------- | ------------------------------------------------------------------ | --------------------------------------------------------------- |
| amountGe                | 0                                                                  | Bottom border of the transferred amount                         |
| amountLe                | 10000000000000000                                                  | Top border of the transferred amount                            |
| chainId                 | 1                                                                  | Id of the event’s chain                                         |
| ethUserAddress          | 0xcbefe3344284444ac8141c930207b8ff82a3177e                         | User address on the ethereum network                            |
| limit                   | 10                                                                 | Maximum number of relayers to be retrieved                      |
| offset                  | 0                                                                  | Offset                                                          |
| ordering                | amountascending                                                    | Value based on which the retrieved relayer data will be ordered |
| relayAddress            | -                                                                  | Address of the relayer                                          |
| roundNum                | 18                                                                 | Round number                                                    |
| timestampGe             | 1642813200000                                                      | Bottom border of the date time of the transfer                  |
| timestampLe             | 1656032400000                                                      | Top border of the date time of the transfer                     |
| tokenAddress            | 0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2 | Address of the transferred token                                |
| tonUserAddress          | 0:1fcdda0bdb6cc28476575f1617949188fb9f29d35b9f86217438baf3519058c3 | User address on the everscale network                           |
| transferContractAddress | 0:91b879d842d2292db57abd10d1cd6e83959dd27fb70189d02032314c0de542a9 | Address of the transfer contract                                |
| transferKind            | ethtoton                                                           | Transfer kind (tontoeth, ethtoton)                              |

