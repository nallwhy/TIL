# `distinct` vs `<>`

Use `distinct`.

```sql
select case when null <> null then true else false end,
case when null != null then true else false end,
case when null is distinct from null then true else false end,
case when null is not distinct from null then true else false end;
```

OR

```sql
select case when null <> null then true else false end,
case when not (null <> null) then true else false end,
case when null is distinct from null then true else false end,
case when null is not distinct from null then true else false end;
```

RETURNS

```
FALSE	FALSE	FALSE	TRUE
```

Reference: https://wiki.postgresql.org/wiki/Is_distinct_from
