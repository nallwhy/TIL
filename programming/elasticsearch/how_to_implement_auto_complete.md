## How to implement **auto complete**

Elastic provides many kinds of `Suggester`, but there is nothing like **auto complete** of Google or Amazon.

그래서 새로 만들었다.

처음에는 [Search like a Google with Elasticsearch. Autocomplete, Did you mean and search for items.](http://www.bilyachat.com/2015/07/search-like-google-with-elasticsearch.html)를 따라 만들었었다. 매우 잘 작동했지만 shingle + 빈도를 기반으로 하는 aggregation 을 이용했기 때문에 index 가 업데이트 될 때마다 새로 데이터를 갱신하게 되어서 document 가 많아지자 매우 느리고 메모리 소비도 심했다.

그래서 원리는 그대로 가져가되 document 로 빈도를 관리하면 aggregation 이 아닌 query 이기 때문에 실시간에 가까운 속도로 처리가 가능할 것이라고 예상해서 새로 작업을 했고 성공적으로 작동하는 것을 확인하였다.

### setting, mapping

실제로 document 들이 들어있는 index 가 있고, suggest 를 위한 index 를 따로 뒀다.

```
@suggest_setting %{
  index: %{
    analysis: %{
      filter: %{
        my_shingle: %{
          type: "shingle",
          min_shingle_size: 2,
          max_shingle_size: 3
        }
      },
      analyzer: %{
        suggest: %{
          type: "custom",
          tokenizer: "standard",
          filter: ["lowercase", "stop", "my_shingle"]
        }
      }
    }
  }
}

@suggest_mapping %{
  product: %{
    properties: %{
      keywords: %{type: "keyword"},
      length: %{type: "long"},
      count: %{type: "long"}
    }
  }
}
```

shingle filter 를 하나 만들어서 min/max single size 를 설정.
analyzer 는 간단하게 lowercaes, stop, shingle filter 를 이용해서 만들었다.

먼저 analyzer 로 shingle 을 생성해내고, 그것을 suggest index 에 document 로 올린다.

이 때 stop filter 와 shinlge filter 를 같이 이용하게 되면 stop 에서 안쓰는 것들을 "_"로 대체한 것을 포함해서 shingle 을 만들어내기 때문에, 그것을 없애기 위해 한 번 처리를 해줬다.

suggest index 에 document 를 등록할 때는, 이미 등록되어있던 keywords 인가 아닌가에 따라 작업이 달라져야 하고 한꺼번에 많이 등록할 수 있어야 한다.
그래서 bulk + upsert + script 조합을 사용하였다.
bulk 를 사용하면 한꺼번에 많이 update 할 수 있다.
upsert 를 사용하면 doc 이 등록되어있을 때와 그렇지 않을 때의 동작을 한꺼번에 처리할 수 있다.
script 를 이용하면 document 를 load 하지 않고도 count 를 늘릴 수 있다.


```
POST _bulk
{ "update" : {"_id" : "hi", "_type" : "product", "_index" : "suggest"} }
{ "script": { "inline": "ctx._source.count++", "lang": "painless"}, "upsert": {"title": "hi", "count": 1}}
{ "update" : {"_id" : "hi", "_type" : "product", "_index" : "suggest"} }
{ "script": { "inline": "ctx._source.count++", "lang": "painless"}, "upsert": {"title": "hi", "count": 1}}
```

query 는 prefix query 를 사용하였다.

```
%{
  size: query.size,
  sort: [%{count: "desc"}, %{length: "asc"}],
  query: %{
    prefix: %{
      keywords: %{value: query.keywords}
    }
  }
}
```

굿!

Reference:  
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/analysis-stop-tokenfilter.html  
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/analysis-shingle-tokenfilter.html  
https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html  
https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update.html  
https://www.elastic.co/guide/en/elasticsearch/reference/5.5/script-processor.html
