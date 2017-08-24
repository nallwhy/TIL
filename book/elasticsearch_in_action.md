## 1.Introduction

ElasticSearch is based on Apache Lucene which is high-performance, full-featured text search engine library written entirely in Java.

### Features

ElasticSearch uses `inverted indexing`.

* The purpose of an inverted index is to allow fast full text searches, at a cost of increased processing when a document is added to the database.

Calculate `relevancy score` usnig an algorithm that based on `tf-idf`(term frequency - inverse document frequence)

- Term frequency: How often the term is in the document. (more often is higher)
- Inverse document frequence: How often the term is in the whole documents. (less often is higher)

You can weight for each score elements.

ElasticSearch is not only for exact match.

- Fuzzy: 오타가 있어도 검색 가능. ex) bicycel -> bicycle
- Analysis: 파생어들을 묶어서 검색 가능. ex) bicyclist, cycling -> bicycle
- Aggregation: 범주별 수치 제공 등. ex) cycling -> bicycle reviews, cycling events
- Suggestion: 제안 제공. ex) bicyc*


## 2. Functions

### Logical structure

`Index` - `Type` - `Document`(identified by ID)

#### Document

- Independent
- Document in document (class)
- Flexsible (schema-free)

```json
{
  "name": "Json",
  "location": {
    "name": "Seoul, Korea"
  },
  "friends": ["Lee", "Mike"]
}
```

#### Type

Schema is not necessary but it's convenient.

#### Index

A container of `Types`. 여러 작업의 범위가 된다. (업데이트, 샤딩 등)


### Searching

#### Result

```json
{
  "took": 2,                    // how long the request takes to reponse
  "timed_out": false,
  "_shards": {
    "total": 2,                 // how many shard that queried
    "successful": 2,
    "failed": 0
  },
  "hits": {
    "total": 2,                 // count of documents of query result
    "max_score": 0.9066504,
    "hits": [
      {
        "_index": "get-together",
        "_type": "group",
        "_id": "3",
        "_score": 0.6055504,
        "fields": {
          "loation": ["Seoul", "Korea"],
          "name": ["Json"]
        }
      }
    ]
  }
}
```

#### Querying

##### `query_string`

```json
{
  "query": {
    "query_string": {
      "query": "elasticsearch san francisco",
      "default_field": "name",
      "default_operator": "AND"
    }
  }
}
```

##### `term`

```json
{
  "query": {
    "term": {
      "name": "elasticsearch"
    }
  }
}
```

##### `filter`

Don't consider scores.

```json
{
  "query": {
    "filtered": {
      "filter": {
        "term": {
          "name": "elasticsearch"
        }
      }
    }
  }
}
```

##### `aggregations`

request
```json
{
  "aggregations": {
    "organizers" : {
      "terms": {
        "field": "organizer"
      }
    }
  }
}
```

result
```json
{
  "aggregations": {
    "organizers" : {
      "buckets": [
        {
          "key": "lee",
          "doc_count": 2
        },
        {
          "key": "andy",
          "doc_count": 1
        }
      ]
    }
  }
}
```

## 3. Data indexing, modifying, deleting

### Indexing

#### Mapping

If you add mapping to `type` which already mapped, those mappings are merged by ElasticSearch.

#### Variable types

string(text, keyword), numeric(byte, short, integer, long, float, double), date, boolean

- text: A field to index full-text values, such as the body of an email or the description of a product. These fields are analyzed, that is they are passed through an analyzer to convert the string into a list of individual terms before being indexed.
- keyword: They are typically used for filtering (Find me all blog posts where status is published), for sorting, and for aggregations. Keyword fields are only searchable by their exact value.

#### Array

You don't have a specific mapping to define array field.

#### Fields

It is often useful to index the same field in different ways for different purposes. This is the purpose of multi-fields.

```json
{
  "mappings": {
    "my_type": {
      "properties": {
        "text": {
          "type": "text",
          "fields": {
            "english": {
              "type":     "text",
              "analyzer": "english"
            }
          }
        }
      }
    }
  }
}
```

#### Pre-defined Field

_timestamp, _ttl(time to live), _source, _all(indexing all field), _size, _id, ...

##### `_all`

`_all` indexes all fields. To reduce the size and imporve query speed, `_all` can be disabled.

```json
"my_type": {
  "_all": {"enabled": false}
}
```

### Modifying

- update
- upsert
- using script

ElasticSearch has version control for documents.

### Deleting

You can delete data by document, type, index. Or you can just **close** index to preserve raw data, then you can **open** it anytime.


## 4. Data searching

```json
{
  "query": {
    "match_all": {}
  },
  "from": 0,
  "size": 10,
  "_source": ["name", "organizer"],
  "sort": [{"created_on": "desc"}]
}
```

### Filter

```json
{
  "query": {
    "filtered": {
      "query": {
        "match": {
          "title": "hadoop"
        }
      }
    }
  },
  "filter": {
    "term": {
      "host": "andy"
    }
  }
}
```

Bitset for filtering can be cached.

#### `match_all`

Match all document. There is the inverse of this query, `match_none`.

#### `query_string`

