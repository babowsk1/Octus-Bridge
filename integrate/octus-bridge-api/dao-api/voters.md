# Voters

{% swagger method="post" path="/proposals/count" baseUrl="https://dao.octusbridge.io/v1/voters" summary="Get proposals count" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
[
  {
    "voter": "0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd",
    "count": 2
  },
  {
    "voter": "0:a381e2e2c8fc8b1a4da9b72d55c8600ba209ea5f01da01c7811d3f38a79204ea",
    "count": 2
  },
  {
    "voter": "0:e5623ad7084d054fb326afaa1eb41288b4ef1f6891d6f4053e09b87e501f03da",
    "count": 2
  }
]
```
{% endswagger-response %}
{% endswagger %}

This function returns the number of proposals each voter took a part in. 

It can be used for displaying the voting activity of each specified user.

### Request parameters

Required body parameters:  

| Name   | Example value                                                      | Comment                   |
|--------|--------------------------------------------------------------------|---------------------------|
| voters | 0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd | List of voters’ addresses |

### Response fields explanation

| Name  | Example value                                                      | Comment                                                   |
|-------|--------------------------------------------------------------------|-----------------------------------------------------------|
| voter | 0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd | Voter’s address                                           |
| count | 2                                                                  | Number of proposals for which certain voter raised a vote |

### Example 

```java
app.post('/voters/proposals/count', (req, res) => {
 
    axios({
        method: 'post',
        url: `${apiUrl}/voters/proposals/count`,
        data: {
            voters: req.body.voters
        }
    })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```

{% swagger method="post" path="/proposals/count/search" baseUrl="https://dao.octusbridge.io/v1/voters" summary="Get proposals count" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
[
  {
    "voter": "0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd",
    "count": 2
  },
  {
    "voter": "0:a381e2e2c8fc8b1a4da9b72d55c8600ba209ea5f01da01c7811d3f38a79204ea",
    "count": 2
  },
  {
    "voter": "0:e5623ad7084d054fb326afaa1eb41288b4ef1f6891d6f4053e09b87e501f03da",
    "count": 2
  }
]
```
{% endswagger-response %}
{% endswagger %}

This function returns ordered list of users with the number of proposals they took part in. 

It can be used to show voter’s activity ordered by a specified column (i.e. createdAt) and the direction (ascending, descending).

### Request parameters

Required body parameters:  

| Name      | Example value                                                      | Comment                                                                  |
|-----------|--------------------------------------------------------------------|--------------------------------------------------------------------------|
| limit     | 5                                                                  | Maximum number of proposals to be retrieved                              |
| offset    |                                                                    | Offset                                                                   |
| ordering  |                                                                    | Set of parameters based on which the retrieved proposals will be ordered |
| column    | count                                                              | Order by given column name (i.e. createdAt)                              |
| direction | ASC                                                                | Order by given direction (ascending or descending)                       |
| voters    | 0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd | List of voters’ addresses                                                |

### Response fields explanation 

| Name  | Example value                                                      | Comment                                                   |
|-------|--------------------------------------------------------------------|-----------------------------------------------------------|
| voter | 0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd | Voter’s address                                           |
| count | 2                                                                  | Number of proposals for which certain voter raised a vote |

### Example

```java
app.post('/voters/proposals/count/search', (req, res) => {
 
    axios({
        method: 'post',
        url: `${apiUrl}/voters/proposals/count/search`,
        data: {
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            voters: req.body.voters
        }
    })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```

{% swagger method="post" path="/{voter}/search" baseUrl="https://dao.octusbridge.io/v1/voters" summary="Get proposals with votes data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "proposalWithVotes": [
    {
      "vote": {
        "proposalId": 6,
        "voter": "0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd",
        "support": true,
        "reason": "",
        "votes": "5061664014",
        "locked": false,
        "messageHash": "0275dde58e1a456e6dbba65aba2f295e2d33812353f0632c9728c084843a3678",
        "transactionHash": "3024c7309609b69cf8ad0f6efc686fb3bf91ccc257261e9063c5cee35ac6f7cf",
        "createdAt": 1654530320
      },
      "proposal": {
        "proposalId": 6,
        "proposalAddress": "0:b0719c636ebd7e5fde1b4c0374dfe1808b46ca47afd2999379fc23cc9ce1edbd",
        "proposer": "0:56629b68a5ac850b5513ec992998a24eb4330d03171db1db91d485133dbe88c2",
        "description": Increase Octusbridge vault limits ... ,
        "startTime": 1654361225,
        "endTime": 1654620425,
        "executionTime": 1654793225,
        "gracePeriod": 172800,
        "timeLock": 172800,
        "votingDelay": 172800,
        "forVotes": "607634505921299",
        "againstVotes": "0",
        "quorumVotes": "500000000000000",
        "messageHash": "530b6645278c64e8c72822f6bd29cb8d890b2196531404b1387fc403cb885d3c",
        "transactionHash": "eb4c542297509c1662e6e6f268e7ab6670605d454cf36628925a1817b644f24a",
        "actions": {
          "tonActions": [
            {
              "value": "1000000000",
              "target": "0:cb5f0cb869c91731da283f5546c42d3a3353e6e260dda170b4650970b62519b0",
              "payload": "te6ccgEBAgEAEQABCAMFmxgBABBBY2NlcHRlZA=="
            }
          ],
          "ethActions": []
        },
        "executed": true,
        "canceled": false,
        "queued": true,
        "executedAt": 1654796642,
        "canceledAt": null,
        "queuedAt": 1654650616,
        "createdAt": 1654188416,
        "state": "Executed"
      }
    }
  ],
  "totalCount": 1
}
```
{% endswagger-response %}
{% endswagger %}

This function returns details about certain proposals based on proposal address, id, proposer’s address, start and end time as well as the proposal’s status (Pending, Executed…). 

It can be used for filtering proposals based on parameters such as proposal id, proposal’s address, proposer’s address, start and end time of the proposal, showing all the details about the searched proposal such as: description, state, information about the votes, execution time, grace period, quorum details, message and transaction hash, etc.

### Request parameters 

| Name   | Example value                                                      | Comment                   |
|--------|--------------------------------------------------------------------|---------------------------|
| voter | 0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd |  represents address of a specific voter |

Required body parameters:  

| Name               | Example value                                                      | Comment                                                                  |
|--------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------|
| voter              | 0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd | represents address of a specific voter                                   |
| availableForUnlock |true| True if vote is available for unlock, false if not                       |
| endTimeGe          |1625747869| Proposals that ended after or during the given time (in UNIX format)     |
| endTimeLe          |1688819869| Proposals that ended before or during the given time (in UNIX format)    |
| limit              |10| Maximum number of proposals to be retrieved                              |
| locked             |false| True if locked, false if not                                             |
| offset             |0| Offset                                                                   |
| ordering           |                                                                    | Set of parameters based on which the retrieved proposals will be ordered |
| column             |createdAt| Order by given column name (i.e. createdAt)                              |
| direction          |ASC| Order by given direction (ascending or descending)                       |
| proposalAddress    |0:b0719c636ebd7e5fde1b4c0374dfe1808b46ca47afd2999379fc23cc9ce1edbd| Address of the desired proposal                                          |
| proposalId         |6| Id of the desired proposal                                               |
| proposer           |0:56629b68a5ac850b5513ec992998a24eb4330d03171db1db91d485133dbe88c2| Address of the user that created the proposal                            |
| startTimeGe        |1625747869| Proposals that started after or during the given time (in UNIX format)   |
| startTimeLe        |1688819869| Proposals that started before or during the given time (in UNIX format)  |
| state              |Executed| State of the proposal (Executed, pending…)                               |
| support            |true| True if voted for, false if voted against the proposal                   |

### Response fields explanation

| Name              | Example value | Comment                                                                |
|-------------------|---------------|------------------------------------------------------------------------|
| proposalWithVotes |               | List of proposals with votes of the certain voter                      |
| proposal          |               | Details about the proposal                                             |
| actions           |               | Details about ethereum and everscale actions                           |
| ethActions        |               | list of all the actions arrived from Everscale with following data:    |
| - callData          |"string"| Additional call data                                                   |
| - chainId           |0| Id of the chain where the action happened                              |
| - signature         |"string"| Relay’s signature                                                      |
| - target            |"string"| Target address                                                         |
| - value             |"string"| Amount of tokens                                                       |
| tonActions        |               | list of all the actions arrived from ethereum side:                    |
| - payload           |te6ccgEBAgEAEQABCAMFmxgBABBBY2NlcHRlZA==| Payload data                                                           |
| - target            |0:cb5f0cb869c91731da283f5546c42d3a3353e6e260dda170b4650970b62519b0| Target address                                                         |
| - value             |1000000000| Amount of tokens                                                       |
| againstVotes      |0| Number of votes against proposal                                       |
| canceled          |false| True if proposal is canceled, false if not                             |
| canceledAt        |null| Date time of canceling event in UNIX format                            |
| createdAt         |1654188416| Date time of proposal’s creation in UNIX format                        |
| description       |Increase Octusbridge vault limits ...| Description of proposal’s motive                                       |
| endTime           |1654620425| Date time of the end of voting in UNIX format                          |
| executed          |true| True if proposal is executed, false if not                             |
| executedAt        |1654796642| Date time of proposal’s actual execution                               |
| executionTime     |1654793225| Predicted execution time in UNIX format                                |
| forVotes          |607634505921299| Number of votes supporting the proposal                                |
| gracePeriod       |172800| Timespan in days for how long will the proposal be in the grace period |
| messageHash       |0275dde58e1a456e6dbba65aba2f295e2d33812353f0632c9728c084843a3678| Hash code of the message                                               |
| proposalAddress   |0:b0719c636ebd7e5fde1b4c0374dfe1808b46ca47afd2999379fc23cc9ce1edbd| Address of the proposal’s contract                                     |
| proposalId        |6| Id of the proposal                                                     |
| proposer          |0:56629b68a5ac850b5513ec992998a24eb4330d03171db1db91d485133dbe88c2| Address of the user that created the proposal                          |
| queued            |true| True if the proposal is queued, false if not                           |
| queuedAt          |1654650616| Date of queuing the proposal                                           |
| quorumVotes       |500000000000000| Number of votes for reaching the quorum                                |
| startTime         |1654361225| Date time of the start of voting                                       |
| state             |Executed| State of the proposal (Executed, Pending…)                             |
| timeLock          |172800| Timespan of the lock of proposal (grace period)                        |
| transactionHash   |eb4c542297509c1662e6e6f268e7ab6670605d454cf36628925a1817b644f24a| Hash code of the transaction                                           |
| votingDelay       |172800| Timespan of the voting delay (grace period)                            |
| vote              |               | createdAt                                                              |
| createdAt         |1654530320| Date time when the vote was raised                                     |
| locked            |false| True if vote is locked, false if not                                   |
| messageHash       |530b6645278c64e8c72822f6bd29cb8d890b2196531404b1387fc403cb885d3c| Hash code of the message                                               |
| proposalId        |6| Id of the proposal voted for                                           |
| reason            |"string"| Reason for voting                                                      |
| support           |true| True if the vote is for, false if it’s against                         |
| transactionHash   |eb4c542297509c1662e6e6f268e7ab6670605d454cf36628925a1817b644f24a| Hash code of the transaction                                           |
| voter             |0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd| Voter’s address                                                        |
| votes             |5061664014| Number of votes given                                                  |
| totalCount        |1| Total number of proposals retrieved                                    |

### Example 

```java
app.post('/voters/:voter/search', (req, res) => {
 
    axios({
        method: 'post',
        url: `${apiUrl}/voters/${req.params.voter}/search`,
        data: {
            availableForUnlock: req.body.availableForUnlock,
            endTimeGe: req.body.endTimeGe,
            endTimeLe: req.body.endTimeLe,
            limit: req.body.limit,
            locked: req.body.locked,
            offset: req.body.offset,
            ordering: req.body.ordering,
            proposalAddress: req.body.proposalAddress,
            proposalId: req.body.proposalId,
            proposer: req.body.proposer,
            startTimeGe: req.body.startTimeGe,
            startTimeLe: req.body.startTimeLe,
            state: req.body.state,
            support: req.body.support
        }
    })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```