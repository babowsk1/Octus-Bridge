# DAO

{% swagger method="post" path="/search/stakeholders" baseUrl="https://api.octusbridge.io/v1/dao" summary="Get stakeholders data." %}
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