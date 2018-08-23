# Upsert on Postgresql

```sql
INSERT INTO tests (column1, column2)
  SELECT source_column, 'data' FROM sources
ON CONFLICT (index_column1, index_column2)
  DO UPDATE SET
    column2 = tests.column2 + 1,
    column3 = 'any value';
```
