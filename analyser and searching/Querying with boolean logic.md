
1. Get all orders from channel "offline" and store "Milano"
2. Get all orders from channel "online" and price greater 100 less than 200
3. Get all orders from Januray through offline mode
4. Get all orders from the customer age ranging between 40 to 60. Exclude the orders from Milano store
5. Get all orders from the where customers age is greater than 40. stores are Milaono or Texas

Solution --

```
GET /orders/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "store": {
              "value": "Milano"
            }
          }
        },
        {
          "term" : {
            "channel": "offline"
          }
        }
      ]
    }
  }
}

```

5.

```
GET /orders/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "bool": {
            "should": [
              {"term": {
                "store": {
                  "value": "Milano"
                }
              }},
              
               {"term": {
                "store": {
                  "value": "Texas"
                }
              }}
            ]
          }
          
        },
        
        {
          "range": {
            "customer.age": {
              "gte": 40,
              "lte": 60
            }
          }
        }
      ]
    }
  }
}

```