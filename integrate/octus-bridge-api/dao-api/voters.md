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

```
{% endswagger-response %}
{% endswagger %}