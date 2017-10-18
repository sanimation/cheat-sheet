# Postgres CheatSheet
## Mode ligne de commande
Se connecter à la base via psql

`$ psql -U <user_name>`

## Lister les bases

```
SELECT datname FROM pg_database;
```

## Backup DB:

Uncompressed backup: 

```
$ sudo -u <user_name> pg_dump > backup_filename.sql
```

Compressed backup: 

```
$ sudo -u <user_name> pg_dump redash | gzip > backup_filename.gz
```

# Backup Your Redash Database and Restore It on a Different Server

Note: This guide assumes that the default database name (redash, but can be postgres) has not been changed.

1. Check the size of your redash database. This can be done by creating a query within redash itself against the ‘Redash metadata’ data source.

```
select t1.datname AS db_name, pg_size_pretty(pg_database_size(t1.datname)) as db_size
from pg_database t1
where t1.datname = 'redash'

```

1. Check the amount of available disk space on your existing server.

```
df -hT

```

1. Backup the existing redash database.

```
sudo -u redash pg_dump redash | gzip > redash_backup.gz

```

1. Transfer the backup to the new server.
2. [Perform a clean install of Redash](#setup-redash-instance-setup) on the new server.
3. Check the amount of available disk space on the new server.

```
df -hT

```

1. Login as postgres user on the new server.

```
sudo -u postgres -i

```

1. drop the current redash database, create a new database named redash, and then restore the backup into the new database.

```
dropdb redash
createdb -T template0 redash
gunzip -c redash_backup.gz | psql redash

```

1. Set a new password of your choosing for the ‘redash_reader’ user (since the new installation generated a random password).

```
psql -c "ALTER ROLE redash_reader WITH PASSWORD 'yourpasswordgoeshere';"

```

Note: Then you must navigate to the ‘Redash metadata’ data source (/data_sources/1) in the new Redash installation and change the password to match the one entered above.

1. Grant permissions on the redash database to the redash_reader user.

```
psql -c "grant select(id,name,type) ON data_sources to redash_reader;" redash
psql -c "grant select(id,name) ON users to redash_reader;" redash
psql -c "grant select on events, queries, dashboards, widgets, visualizations, query_results to redash_reader;" redash

```

Create a new query in redash (using Redash metadata as the data source) to test that everything is working as expected.
