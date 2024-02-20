
## Importing data into local cluster

```
# Without CA certificate validation. This is fine for development clusters, but don't do this in production!

curl -k -u elastic -H "Content-Type:application/x-ndjson" -XPOST https://ec2-52-91-132-204.compute-1.amazonaws.com:9200/_bulk --data-binary "@orders.bulk.ndjson"
curl -k -u elastic -H "Content-Type:application/x-ndjson" -XPOST https://ec2-52-91-132-204.compute-1.amazonaws.com:9200/_bulk --data-binary "@nginx-access-logs-2020-01.bulk.ndjson"
curl -k -u elastic -H "Content-Type:application/x-ndjson" -XPOST https://ec2-52-91-132-204.compute-1.amazonaws.com:9200/_bulk --data-binary "@nginx-access-logs-2020-02.bulk.ndjson"
curl -k -u elastic -H "Content-Type:application/x-ndjson" -XPOST https://ec2-52-91-132-204.compute-1.amazonaws.com:9200/_bulk --data-binary "@nginx-access-logs-2020-03.bulk.ndjson"

# With CA certificate validation. The certificate is located at $ES_HOME/config/certs/http_ca.crt
curl --cacert /path/to/http_ca.crt -u elastic -H "Content-Type:application/x-ndjson" -XPOST http://ec2-52-91-132-204.compute-1.amazonaws.com:9200/_bulk --data-binary "@orders.bulk.ndjson"
curl --cacert /path/to/http_ca.crt -u elastic -H "Content-Type:application/x-ndjson" -XPOST http://ec2-52-91-132-204.compute-1.amazonaws.com:9200/_bulk --data-binary "@nginx-access-logs-2020-01.bulk.ndjson"
curl --cacert /path/to/http_ca.crt -u elastic -H "Content-Type:application/x-ndjson" -XPOST http://ec2-52-91-132-204.compute-1.amazonaws.com:9200/_bulk --data-binary "@nginx-access-logs-2020-02.bulk.ndjson"
curl --cacert /path/to/http_ca.crt -u elastic -H "Content-Type:application/x-ndjson" -XPOST http://ec2-52-91-132-204.compute-1.amazonaws.com:9200/_bulk --data-binary "@nginx-access-logs-2020-03.bulk.ndjson"
```


