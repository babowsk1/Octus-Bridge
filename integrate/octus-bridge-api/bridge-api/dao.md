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

