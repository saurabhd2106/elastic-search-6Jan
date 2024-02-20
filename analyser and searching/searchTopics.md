**Searching a document**

1. query - matchall

```
GET /access-logs-2020-01/_search
{
  "query": {
    "match_all": {
      
    }
  }
}

```

2.  query - term and terms

```
GET /access-logs-2020-01/_search
{
  "query": {
    "term": {
      "client.geo.country_name": {
        "value": "united states",
        "case_insensitive": true
      }
    }
  }
}

```

```

GET /access-logs-2020-01/_search
{
  "query": {
    "terms": {
      "FIELD": [
        "Unites States",
        "Israel"
      ]
    }
  }
}

```

