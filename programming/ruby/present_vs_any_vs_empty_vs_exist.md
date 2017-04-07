## Faster Rails: How to Check if a Record Exists

https://semaphoreci.com/blog/2017/03/14/faster-rails-how-to-check-if-a-record-exists.html

### Existence checks in Rails

```ruby
Build.where(:created_at => 7.days.ago..1.day.ago).passed.present?

# SELECT "builds".* FROM "builds" WHERE ("builds"."created_at" BETWEEN
# '2017-02-22 21:22:27.133402' AND '2017-02-28 21:22:27.133529') AND
# "builds"."result" = $1 [["result", "passed"]]


Build.where(:created_at => 7.days.ago..1.day.ago).passed.any?

# SELECT COUNT(*) FROM "builds" WHERE ("builds"."created_at" BETWEEN
# '2017-02-22 21:22:16.885942' AND '2017-02-28 21:22:16.886077') AND
# "builds"."result" = $1 [["result", "passed"]]


Build.where(:created_at => 7.days.ago..1.day.ago).passed.empty?

# SELECT COUNT(*) FROM "builds" WHERE ("builds"."created_at" BETWEEN
# '2017-02-22 21:22:16.885942' AND '2017-02-28 21:22:16.886077') AND
# "builds"."result" = $1 [["result", "passed"]]


Build.where(:created_at => 7.days.ago..1.day.ago).passed.exists?

# SELECT 1 AS one FROM "builds" WHERE ("builds"."created_at" BETWEEN
# '2017-02-22 21:23:04.066301' AND '2017-02-28 21:23:04.066443') AND
# "builds"."result" = $1 LIMIT 1 [["result", "passed"]]
```

 `.present?` is very inefficient. It loads **all the records** from the database into memory, constructs the Active Record objects, and then finds out if the array is empty or not.

 `any?` and `empty?`, are optimized in Rails and load only `COUNT(*)` into the memory. `COUNT(*)` queries are usually efficient, and you can use them even on semi-large tables without any dangerous side effects.

 `exists?`, is even more optimized, and it should be your first choice when checking the existence of a record. It uses the `SELECT 1 ... LIMIT 1` approach, which is very fast.

```
present? =>  2892.7 ms
any?     =>   400.9 ms
empty?   =>   403.9 ms
exists?   =>     1.1 ms
```

### Exception

If we are checking for the existence of an association record without any scope, `any?` and `empty?` will also produce a very optimized query that uses `SELECT 1 FROM ... LIMIT 1` form, but `any?` fill not hit the database again if the records are **already loaded** into memory.


```ruby
project = Project.find_by_name("semaphore")

project.builds.load    # eager loads all the builds into the association cache

project.builds.any?    # no database hit
project.builds.exists? # hits the database

# if we bust the association cache
project.builds(true).any?    # hits the database
project.builds(true).exists? # hits the database
```
