## Fixing `psql: could not connect to server` Error

Sometimes you should encounter the error below if you use postgresql.

```bash
$ psql
psql: could not connect to server: No such file or directory
    Is the server running locally and accepting
    connections on Unix domain socket "/tmp/.s.PGSQL.5432"?
```

As there are many reasons of that problem, I will introduce some ways.

### Remove pid file of postgresql

```bash
$ rm /usr/local/var/postgres/postmaster.pid
```

### Remove and Init DB

You will loose your data on the db.

```bash
$ rm -rf /usr/local/var/postgres && initdb /usr/local/var/postgres -E utf8
```

Reference:
http://stackoverflow.com/questions/13410686/postgres-could-not-connect-to-server
