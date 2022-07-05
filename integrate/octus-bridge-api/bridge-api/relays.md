# Relays

{% swagger method="post" path="/relay_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get relayer info" %}
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
  "relayTotalConfirmed": 7156,
  "potentialTotalConfirmed": 8403,
  "evmStats": [
    {
      "chainId": 1,
      "relayConfirmed": 1774,
      "potentialConfirmed": 2045
    },
    ...
 {
      "chainId": 43114,
      "relayConfirmed": 105,
      "potentialConfirmed": 123
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

This function is used be used to get relayer info.

Returns information about a specific relayer based on his address. It can be used anywhere where details about a specific relayer is needed such as details about events and their confirmation, relay rounds, rewards, stake etc.

### Request parameters

Required body parameters:  

### Response fields explanation:



### Example

```java
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
```

{% swagger method="post" path="/relay_round_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get relayer round info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
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

The function is used to get relayer's round info.

Returns list of relayers and details about them based on the round number they are part of. It can be used for listing all or certain number of relayers when it comes to one relay round. Some of the details about the relayers are number of confirmed events and the share per event, relay’s address, list of events, place of a relayer and also info about the round such as start and end time, round number and address, etc.

### Request parameters

Required body parameters:  


### Response fields explanation:



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

{% swagger method="post" path="/all_relay_rounds_info" baseUrl="https://api.octusbridge.io/v1/relays_pages" summary="Get all relayer's rounds info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
