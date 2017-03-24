## Updating the mappings and settings of an existing index

To update the **settings**, if you're defining new analyzers or filters, you first need to `_close` the index, then `_open` it when done updating:

```
$ curl -X POST 'http://localhost:9200/thegame/_close'

$ curl -X PUT 'http://localhost:9200/thegame/_settings' -d \
'{
  "analysis": {
    "analyzer": {
      "full_name": {
        "filter": [
          "standard",
          "lowercase",
          "asciifolding"
        ],
          "type": "custom",
          "tokenizer": "standard"
      }
    }
  }
}'

$ curl -X POST 'http://localhost:9200/thegame/_open'
```

To update the **mappings** of this existing index, you need to do it **for each type** (here we only have the weapons type):

```
$ curl -X PUT 'http://localhost:9200/thegame/weapons/_mapping?ignore_conflicts=true' -d \
'{
  "weapons": {
    "properties": {
      "name": {
        "type": "text",
        "analyzer": "full_name"
      },
      "description": {
        "type": "text"
      },
      "category": {
        "type": "text"
      }
    }
  }
}'
```

You can do all of this at once if you delete then re-create your index, but you will loose all stored documents, so you will have to reload them.

Reference: https://gist.github.com/nicolashery/6317643

=======

I failed to close index on `Elastic Cloud`.

I found a document about `open/close index`.

>Closed indices consume **a significant amount of disk-space** which can cause problems in managed environments. Closing indices can be disabled via the cluster settings API by setting `cluster.indices.close.enable` to `false`. The default is `true`.

It says the default of `cluster.indices.close.enable` is `true`.

But in Elastic Cloud document, it's not!

>`cluster.indices.close.enable` - enables closing indices in Elasticsearch version 2.2 and later. We strongly recommend leaving this set to `false` (the **default**). Closed indices are a data loss risk: If you close an index, it is not included in snapshots and you will not be able to restore the data. Similarly, closed indices are not included when you scale to a different cluster size or during failover operations.  
*You might enable this setting temporarily in order to change the analyzer configuration for an existing index.*

[Jongmin](https://www.facebook.com/kimjmin81) said close/open index is not so different of dump/restore snapshot or reindexing.

And because Elastic Cloud controls many things automatically, it's more dangerous than other ways on it.


Reference:  
https://gist.github.com/nicolashery/6317643  
https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-open-close.html  
https://www.elastic.co/guide/en/cloud/external/cluster-config.html#user-settings
https://discuss.elastic.co/t/how-can-i-enable-cluster-indices-close-enable-temporarily/79543