# DAO

{% swagger method="post" path="/search/stakeholders" baseUrl="https://api.octusbridge.io/v1/dao" summary="Get stakeholders data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "stakeholders": [
    {
      "userAddress": "0:0a75c8fa5a9efa817eda3fcd51717d9690cc7ec989881fecb73616f249b8fbce",
      "votes": "0",
      "voteWeight": "0",
      "proposalVotesCount": 1
    },
    ...
{
      "userAddress": "0:8e17dbaa03a309b9f05867595126a72e5cbbe8c61d10f1250fb8d9753aaf0f7d",
      "votes": "0",
      "voteWeight": "0",
      "proposalVotesCount": 0
    }
  ],
  "totalCount": 206
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get stakeholders data.

It can be used for showing a list of desired number of stakeholders, where the information about total number of votes a stakeholder raised, how much stakeholder’s vote can weigh, address and number of proposals he voted for ordered by the vote weight.

### Request parameters:

Required body parameters:

| Name     | Example value         | Comment                                                                                                                                                                                                                      |
| -------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| limit    | `50`                  | Maximum number of stakeholders to be retrieved                                                                                                                                                                               |
| offset   | `0`                   | Offset                                                                                                                                                                                                                       |
| ordering | `voteweightascending` | Value based on which the retrieved stakeholders data will be ordered (voteweightascending, voteweightdescending…)based on which the retrieved stakeholders data will be ordered (voteweightascending, voteweightdescending…) |

### Response fields explanation:



| Name               | Example value                                                        | Comment                                                          |
| ------------------ | -------------------------------------------------------------------- | ---------------------------------------------------------------- |
| stakeholders       | -                                                                    | List of stakeholders data determined by the limit body parameter |
| proposalVotesCount | `1`                                                                  | Amount of proposals stakeholder raised a vote                    |
| userAddress        | `0:0c3fbf8b400ce637a49e09e7ae2fc5e92920680b1d10f4cd6956c7aebde93903` | Address of the stakeholder                                       |
| voteWeight         | `0`                                                                  | Amount per vote                                                  |
| votes              | `0`                                                                  | Total amount of votes raised                                     |
| totalCount         | `208`                                                                | Total number of stakeholders                                     |

### Example

```java
app.post('/dao/search/stakeholders', (req, res) => {
    axios({
        method: 'post',
        url: `${apiUrl}/dao/search/stakeholders`,
        data: {
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering
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

{% swagger method="get" path="/user/{user_address}" baseUrl="https://api.octusbridge.io/v1/dao" summary="Get stakeholder data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```python
{
  "userAddress": "0:66003d2db4bc1566c3d7d3c118004b1e1d54f1f62c30c6b173845db3aa459f07",
  "votes": "100002.580351726000",
  "voteWeight": "3.4000",
  "proposalVotesCount": 1
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get stakeholder data.

It can be used to show one’s stakeholder data based on his account address. Information that can be displayed is the amount of votes certain stakeholder raised, his vote weight, address and total number of proposal votes.

### Request parameters:

Required parameters:

| Name        | Example Value                                                      | Comment                       |
| ----------- | ------------------------------------------------------------------ | ----------------------------- |
| userAddress | 0:66003d2db4bc1566c3d7d3c118004b1e1d54f1f62c30c6b173845db3aa459f07 | Address of particular account |

### Response fields explanation:



| Name               | Example value                                                      | Comment                                        |
| ------------------ | ------------------------------------------------------------------ | ---------------------------------------------- |
| proposalVotesCount | 1                                                                  | Amount of proposals stakeholder raised a vote  |
| userAddress        | 0:66003d2db4bc1566c3d7d3c118004b1e1d54f1f62c30c6b173845db3aa459f07 | Address of the user                            |
| voteWeight         | 3.400                                                              | Amount representing the vote weight (per vote) |
| votes              | 100002.580351726000                                                | Total amount of votes raised                   |

### Example

```java
app.get('/dao/user/:user_address', (req, res) => {
    axios({
        method: 'get',
        url: `${apiUrl}/dao/user/${req.params.user_address}`
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

{% swagger method="post" path="/relay_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get relayer's info" %}
{% swagger-description %}
****
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

This function is used to return information about a specific relay based on its address.

&#x20;It can be used anywhere where details about a specific relayer is needed such as details about events and their confirmation, relay rounds, rewards, stake etc.

### Request parameters:

Required body parameters:

| Name         | Example value                                                      | Comment                        |
| ------------ | ------------------------------------------------------------------ | ------------------------------ |
| relayAddress | 0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557 | Address of the desired relayer |

### Response fields explanation:

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

This function use to get relayer round info.

It can be used for showing a relayer’s efforts in one specific round. \
Following data about the relayer’s performance based on the round number can be displayed: \
How much a relayer staked to become a relayer, number of events he confirmed, volume from all the transfers relayer validated happened from everscale to ethereum network and vice versa shown in USDTs, round address, start and end time of the round

### Request parameters:

Required body parameters:

| Name         | Example value                                                      | Comment                        |
| ------------ | ------------------------------------------------------------------ | ------------------------------ |
| relayAddress | 0:daacff0f136da1d5c9fa73200d481362c44756b0ff7d083ee02e95f00a078557 | Address of the desired relayer |

### Response fields explanation:



| Name                 | Example value                                                      | Comment                                                                             |
| -------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| endTime              | 1654604726000                                                      | Date time of the relay round’s end                                                  |
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
