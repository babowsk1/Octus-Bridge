# Votes

{% swagger method="post" path="/search" baseUrl="https://dao.octusbridge.io/v1/votes" summary="Get votes data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "votes": [
    {
      "proposalId": 6,
      "voter": "0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd",
      "support": true,
      "reason": "",
      "votes": "5061664014",
      "locked": false,
      "messageHash": "0275dde58e1a456e6dbba65aba2f295e2d33812353f0632c9728c084843a3678",
      "transactionHash": "3024c7309609b69cf8ad0f6efc686fb3bf91ccc257261e9063c5cee35ac6f7cf",
      "createdAt": 1654530320
    }
  ],
  "totalCount": 1
}
```
{% endswagger-response %}
{% endswagger %}

This function returns voting details of a specific user based on a specific proposal.

It can be used for showing detailed information about a user's vote such as number of votes raised for a specified proposal, reason for voting, did the user support the proposal or not, time of voting etc.

### Request parameters

Required body parameters:

| Name       | Example value                                                      | Comment                                                                  |
| ---------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| limit      | 5                                                                  | Maximum number of proposals to be retrieved                              |
| locked     | false                                                              | True if locked, false otherwise                                          |
| offset     | 0                                                                  | Offset                                                                   |
| ordering   |                                                                    | Set of parameters based on which the retrieved proposals will be ordered |
| column     | createdAt                                                          | Order by given column name (i.e. createdAt)                              |
| direction  | ASC                                                                | Order by given direction (ascending or descending)                       |
| proposalId | 6                                                                  | Id of the proposal                                                       |
| support    | true                                                               | True if voted for, false if voted against the proposal                   |
| voter      | 0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd | Voter’s address                                                          |

### Response fields explanation

| Name            | Example value                                                      | Comment                                                              |
| --------------- | ------------------------------------------------------------------ | -------------------------------------------------------------------- |
| totalCount      |                                                                    | Total number of times voter voted for a specific proposal            |
| votes           | 5061664014                                                         | List of all the votes from a specific voter to the specific proposal |
| createdAt       | 1654530320                                                         | Date when the vote was raised                                        |
| locked          | false                                                              | True if vote is locked, false otherwise                              |
| messageHash     | 0275dde58e1a456e6dbba65aba2f295e2d33812353f0632c9728c084843a3678   | Hash code of the message                                             |
| proposalId      | 6                                                                  | Id of the proposal                                                   |
| reason          | ""string""                                                         | Reason for voting                                                    |
| support         | true                                                               | True if voter voted for, false if voted against                      |
| transactionHash | 3024c7309609b69cf8ad0f6efc686fb3bf91ccc257261e9063c5cee35ac6f7cf   | Hash code of the transaction                                         |
| voter           | 0:99ea964906c807e89ff8e55ba96a86e4d85d8020c8365ded9428777aef4281cd | Voter’s address                                                      |
| votes           | 5061664014                                                         | Amount staked for voting                                             |

### Example

```java
app.post('/votes/search', (req, res) => {
 
    axios({
        method: 'post',
        url: `${apiUrl}/votes/search`,
        data: {
            limit: req.body.limit,
            locked: req.body.locked,
            offset: req.body.offset,
            ordering: req.body.ordering,
            proposalId: req.body.proposalId,
            support: req.body.support,
            voter: req.body.voter
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
