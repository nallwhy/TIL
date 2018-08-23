# Create Date index with Timestamp field

Timestamp field must be **without** time zone because it's date should be **IMMUTABLE**.

```sql
CREATE INDEX ON <table> ((<timestamp_field>::DATE));
```

Reference: https://stackoverflow.com/questions/34724403/postgresql-create-an-index-on-timestampdate
