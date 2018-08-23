# Triggers are triggered after a commands and hold its value at that time

trigger function 안에서 delete 를 하고 있지만, 이미 지워진 record 의 after trigger 는 문제없이 실행된다.

```sql
CREATE TABLE tests (id integer PRIMARY KEY, value0 integer, value1 integer);

CREATE OR REPLACE FUNCTION after_trg() RETURNS trigger AS $$
BEGIN
  RAISE NOTICE '%', NEW;
  UPDATE tests SET value1 = value1 + 1 WHERE id = NEW.id;
  DELETE FROM tests WHERE id in (1, 2);

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER tests_after_trg
AFTER UPDATE OF value0 ON tests
FOR EACH ROW
EXECUTE PROCEDURE after_trg();

INSERT INTO tests (id, value0, value1) VALUES (1, 1, 1), (2, 2, 2);

UPDATE tests SET value0 = value0 + 1;

SELECT * FROM tests;

DROP TABLE tests;
```
