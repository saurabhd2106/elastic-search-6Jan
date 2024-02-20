Metric Aggregation

1. Get the sum of all the order price
2. Get the average of all the order price
3. Get the min, max values of the order price
4. Get the count of unique customers

```
GET /orders/_search
{
  "query": {
    "match_all": {
      
    }
  }
}

GET /orders/_search
{
  "size": 0, 
  "query": {
    "match_all": {
      
    }
  },
  
  "aggs": {
    "total_stats": {
      "stats": {
        "field": "total"
      }
    }
  }
  
  
}

GET /orders/_search
{
  "size": 0, 
  "query": {
    "match_all": {
      
    }
  },
  
  "aggs": {
    "total_revenue": {
      "sum": {
        "field": "total"
      }
    },
    "average_revenue": {
      "avg": {
        "field": "total"
      }
    },
    "max_order_value": {
      "max": {
        "field": "total"
      }
    },
    "min_order_value": {
      "min": {
        "field": "total"
      }
    }
  }
  
  
}


GET /orders/_search
{
  "size": 0,
  "aggs": {
    "unique_customers": {
      "cardinality": {
        "field": "customer.id"
      }
    }
  }
  
}







```

```
GET /orders/_search
{
  "size": 0, 
  "query": {
    "match_all": {}
  },
  
  "aggs": {
    "total": {
      "avg": {
        "field": "total"
      }
    }
  }
}



```

Bucket Aggregations

1. Create a bucket with different store types and their document counts

```
GET /orders/_search
{
  "size": 0, 
   "aggs" : {
     "store_name" : {
       "terms": {
         "field": "store",
         "missing": "n/a"
       }
     }
   }
}

```

2. Nested Aggregation

```
GET /orders/_search
{
  "size": 0, 
   "aggs" : {
     "store_name" : {
       "terms": {
         "field": "store",
         "missing": "n/a"
       },
       
       "aggs": {
         "store_stats" : {
           "stats" : {
           "field" : "total"
         }
         }
       }
     }
   }
}
```

