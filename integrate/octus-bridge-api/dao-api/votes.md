# Votes

{% swagger method="post" path="/search" baseUrl="https://dao.octusbridge.io/v1/votes" summary="Get proposals with votes data" %}
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
