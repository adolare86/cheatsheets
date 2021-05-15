## Overview of Elasticsearch API commands

### cat API

#### Health of the cluster
```
curl http://localhost:9200/_cat/_cat/health?v
```

#### Details of shard allocation and disk space uses of each data node
```
curl http://localhost:9200/_cat/allocation?v
```

#### Detailed view of what nodes contain which shards.
```
/_cat/shards?h=index,shard,prirep,state,unassigned.reason
/_cat/shards/twitt*
curl http://localhost:9200/_cat/shards?v
```

#### Displays the master’s node ID, bound IP address, and node name.D
```
curl http://localhost:9200/_cat/master?v
```

#### Detailed info of Cluster nodes
```
/_cat/nodes?v&h=id,ip,port,v,m
curl http://localhost:9200/_cat/nodes?v
```

#### Details of  of each index.
```
curl http://localhost:9200/_cat/indices?v
curl 'localhost:6060/_cat/indices?v&health=yellow'
```

#### Shows on-going and completed index shard recoveries
```
/_cat/recovery?v&h=name,id,pid,ip
curl http://localhost:9200/_cat/recovery?v
```

#### Shows cluster-wide thread pool statistics per node
```
/_cat/thread_pool?v&h=id,pid,ip
curl http://localhost:9200/_cat/thread_pool?v

```
#### Shows snapshots belonging to a repository
```
curl http://localhost:9200/_cat/snapshots/my_repo?v

```
#### Provides information about existing templates
```
/_cat/templates/my_template
curl http://localhost:9200/_cat/templates?v

```
#### Elasticsearch query
```
curl -X GET ‘http://XXX.XXX.XXX.XX:9200/elk_access_log_20170701/_count?' -d ‘{“query”:{“term”:{“apache2.access.response_code”:{“value”:500}}}}’


### Index operation

```
#### Open index
```
curl -XPOST "localhost:6060/logstash-2017.10.1*/_open"
curl -XPOST "localhost:6060/logstash-2019.01.0*/_open"

```
#### Close index
```
curl -XPOST "localhost:6060/logstash-2017.09.01.*/_close?master_timeout=5m"
curl -XPOST "localhost:6060/logstash-2017.10.[11-15].*/_close"

```
#### Create Index
```
curl -XPUT http://localhost:6060/logstash-test

```
#### Delete indices
```
curl -XDELETE -uadmin:$ES_PASS localhost:9200/filebeat-2016.06.14?master_timeout=5m
curl -XDELETE 'http://localhost:6060/logstash-2019.03.0*.*/'
curl -XDELETE 'http://localhost:6060/logstash-2017.*/'
curl -XDELETE 'http://localhost:6060/logstash-2017.05*/'
curl -XDELETE 'http://localhost:6060/logstash-2017.0[1-8]*/'
curl -XDELETE 'http://localhost:6060/logstash-2018.0[8-9].*/?master_timeout=2m'


```
#### Index stats
```
curl localhost:6060/_stats
curl localhost:6060/index1,index2/_stats
curl "localhost:6060/logstash-2017.07.31*/_stats?v"
curl "localhost:6060/_cat/indices?v"
curl -XGET 'http://localhost:6060/logstash-2017.08.03.07/_settings?pretty'

### template operation

```
#### Get template
```
curl -XGET localhost:6060/_template/logstash?pretty > logstash-template.json
 - remove 2 and 3 lines
   "logstash" : {
    "order" : 0,
- add number of shard count in settings > index

```
#### Update template
```
curl -XPUT localhost:6060/_template/logstash -d "@logstash-template.json"

```
#### Delete template
```
curl -XDELETE localhost:9200/_template/logstash-index

```
#### Update replica count
```
curl -XPUT 'localhost:6060/filebeat-7.9.0-2020.08.27-000001/_settings' -d '
    {
        "index" : {
            "number_of_replicas" : 0
        }
    }'

```
#### Cluster allocation
```
curl localhost:6060/_cluster/allocation/explain?pretty

```
#### Reassign shards
```
curl -XPOST 'localhost:6060/_cluster/reroute' -d '{
    "commands": [{
        "allocate": {
            "index": "logstash-2018.10.22",
            "shard": 0,
            "node": "test-node",
            "allow_primary": 1
        }
    }]
}'


```
#### Reassign empty primary shards
```
curl -XPOST "http://localhost:6060/_cluster/reroute" -d' { "commands" : [{ "allocate_empty_primary" : { "index" : "logstash-2019.07.19", "shard" : 0,  "node" : "192.168.10.1", "accept_data_loss": "true" } }] }'

```
#### Reassign replica shards
```
curl -XPOST "http://localhost:6060/_cluster/reroute" -d' { "commands" : [{ "allocate_replica" : { "index" : "logstash-2019.09.21.08", "shard" : 0,  "node" : "192.168.10.1" } }] }'

```
#### Move shards
```
curl -XPOST "http://localhost:6060/_cluster/reroute" -d'
{
    "commands" : [ {
          "move" : {
              "index" : "logstash-2019.10.09", "shard" : 2, "from_node" : "192.168.10.1",  "to_node" : "192.168.10.2"
          }
        }
    ]
}'


```
#### Update mapping field limit
```
curl -XPUT 'localhost:6060/logstash-element-2018.05.05/_settings' -d '
{ "settings" : { "index.mapping.total_fields.limit": 7000 } }'

```
#### Update shards per node 
```
curl -XPUT localhost:6060/test/_settings -d '{
  "index.routing.allocation.total_shards_per_node": 1
}'

```
#### update refresh interval for index
```
curl -XPUT localhost:6060/logstash-element-2018.11.01/_settings -d '{
    "index" : {
        "refresh_interval" : "15s"
    } }'

```
#### Update replicas for index	
```
curl -XPUT 'localhost:6060/logstash-element-2019.10.08/_settings' -d '{
  "number_of_replicas": 0
}'


```
#### Cluster Route allocation enable and disable
```
curl -XPUT 'http://localhost:6060/_cluster/settings' -d '{
    "transient" : {
        "cluster.routing.rebalance.enable" : "none"
    }
}'

curl -XPUT 'http://localhost:6060/_cluster/settings' -d '{
    "transient" : {
        "cluster.routing.allocation.enable" : "all"
    }
}'

PUT _cluster/settings
{
  "transient" : {
    "cluster.routing.allocation.enable": "none",
    "cluster.routing.rebalance.enable" : "none"
  }
}

```
#### After bouncing ES cluster
```
PUT _cluster/settings
{
  "transient" : {
    "cluster.routing.allocation.enable": "all",
    "cluster.routing.rebalance.enable" : "all"
  }
}

```
#### Exclude server for assigning shards
```
curl -XPUT localhost:9200/_cluster/settings -H 'Content-Type: application/json' -d '{
  "transient" :{
      "cluster.routing.allocation.exclude._ip" : "node_ip"
   }
}';


```
#### Update ingest pipeline
```
curl -s -H 'Content-Type: application/json' -XPUT localhost:6060/_ingest/pipeline/server -d@a.json

curl -XPUT localhost:9200/_ingest/pipeline/lowercase-example -d '{
  "processors" : [
    {
      "lowercase" : {
        "field": "message"
      }
    }
  ]
}'

```
#### Update allocation disk watermark limit
```
curl -XPUT 'localhost:6060/_cluster/settings' -d '{
"transient": {
      "cluster.routing.allocation.disk.watermark.low": "100gb",
      "cluster.routing.allocation.disk.watermark.high": "50gb"
}
}'

```
#### Recovery speed
```
curl -XPUT 'localhost:6060/_cluster/settings' -d '{
"transient": {
      "indices.recovery.max_bytes_per_sec" : "10mb"
}
}'

```
#### stop being read-only
```
```curl -XPUT  http://localhost:6060/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'```

