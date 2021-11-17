# Postgres

## Open cli to database

```bash
psql -h localhost -p 30432 -U postgres [-d database]
```

## List databases

```psql
\l
```

## Change db

```psql
\c database
```

## List users

```psql
\du
```

## Quit clli

```psql
\q
```

## Restore dump

```bash
psql -U <user> -c "SELECT pid, (SELECT pg_terminate_backend(pid)) as killed from pg_stat_activity WHERE datname = '<db_name>';"
dropdb -U <user> <db_name>
createdb -U <user> <db_name>
pg_restore -U <user> -j 16 -F c -d <db_name> <dumpfile>
```