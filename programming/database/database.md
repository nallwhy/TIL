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