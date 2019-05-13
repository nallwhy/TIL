### 2018-12-20

#### Principles and Optimization of 5 PostgreSQL Indexes (btree,hash,gin,gist,and brin)

https://medium.com/@Alibaba_Cloud/principles-and-optimization-of-5-postgresql-indexes-btree-hash-gin-gist-and-brin-4d133e7f1842


#### pev

Visualize explains of Postgresql

http://tatiyants.com/pev/#/plans/new


### 2018-10-09

#### `IS NULL` with row

https://dba.stackexchange.com/questions/157691/x-is-not-null-vs-not-x-is-null-in-postgresql


### 2018-08-26

#### Design Patterns using Amazon DynamoDB

https://www.slideshare.net/AmazonWebServices/design-patterns-using-amazon-dynamodb


### 2018-02-27

#### Materialized views in Ecto

https://medium.com/@kaisersly/materialized-views-in-ecto-8887bc89efa5


### 2018-02-09

#### Pagination Done the PostgreSQL Way

http://leopard.in.ua/2014/10/11/postgresql-paginattion


### 2017-12-20

#### PgModeler

https://www.pgmodeler.com.br/


### 2017-11-12

#### The many faces of DISTINCT in PostgreSQL

https://medium.com/statuscode/the-many-faces-of-distinct-in-postgresql-c52490de5954


### 2017-09-12

#### Random sampling

https://stackoverflow.com/questions/8674718/best-way-to-select-random-rows-postgresql  
https://www.postgresql.org/docs/current/static/tsm-system-rows.html


### 2017-08-10

#### PgHero

A performance dashboard for Postgres

https://github.com/ankane/pghero


### 2017-04-05

#### TimescaleDB

https://www.timescale.com/

An open-source time-series database optimized for fast ingest and complex queries. Looks, feels, speaks like Postgres.


### 2017-03-23

#### Hash indexes are faster than Btree indexes?

https://amitkapila16.blogspot.kr/2017/03/hash-indexes-are-faster-than-btree.html

This blog will mainly focus on the search operation. By definition, hash indexes are O(1) and Btree indexes are O(log n), however with duplicates that is not exactly true.

The important thing to note about the above data is that it is only on some of the specific workloads and it mainly covers Selects as that is the main area where performance improvement work has been done for PostgreSQL10.