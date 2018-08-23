# Performance of UPSERT vs INSERT and UPDATE

Exactly the same.

Code:
```sql
CREATE TABLE tests (id integer PRIMARY KEY, value integer);

-- UPSERT
DO $$
DECLARE
  n int := 0;
BEGIN
  LOOP
    n := n + 1;

    INSERT INTO tests (id, value)
    VALUES (trunc(1000 * random()), 1)
    ON CONFLICT (id)
      DO UPDATE SET value = tests.value + 1;

    EXIT WHEN n = 500000;
  END LOOP;

  RETURN;
END$$;

-- INSERT and UPDATE
INSERT INTO tests (id, value)
  SELECT g.id, 0 FROM generate_series(0, 1000) AS g (id) ;

DO $$
DECLARE
  n int := 0;
  v_id int;
BEGIN
  LOOP
    n := n + 1;

    v_id := trunc(1000 * random());
    UPDATE tests SET value = value + 1 WHERE id = (select trunc(1000 * random()));

    EXIT WHEN n = 10;
  END LOOP;

  RETURN;
END$$;

-- check
SELECT count(*), sum(value) FROM tests;

DROP TABLE tests;
```
