## Creating user `postgres` and add role to the account on postgresql

If you install postgresql on Mac via **Homebrew**, the name of default user is user name of Mac.

```
$ psql postgres

postgres=# CREATE ROLE postgres WITH LOGIN PASSWORD '';
postgres=# ALTER ROLE postgres CREATEDB;
postgres=# \du

                                  List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 <user>    | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 postgres  | Create DB                                                  | {}
```

Reference: https://www.codementor.io/devops/tutorial/getting-started-postgresql-server-mac-osx
