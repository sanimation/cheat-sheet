
Se connecter à la base via psql

```
$ psql -U postgres
```

## Backup Your Redash Database and Restore It on a Different Server

Note: This guide assumes that the default database name (redash) has not been changed.

Check the size of your redash database. This can be done by creating a query within redash itself against the ‘Redash metadata’ data source.
select t1.datname AS db_name, pg_size_pretty(pg_database_size(t1.datname)) as db_size
from pg_database t1
where t1.datname = 'redash'
Check the amount of available disk space on your existing server.
df -hT
Backup the existing redash database.
sudo -u redash pg_dump redash | gzip > redash_backup.gz
Transfer the backup to the new server.
Perform a clean install of Redash on the new server.
Check the amount of available disk space on the new server.
df -hT
Login as postgres user on the new server.
sudo -u postgres -i
drop the current redash database, create a new database named redash, and then restore the backup into the new database.
dropdb redash
createdb -T template0 redash
gunzip -c redash_backup.gz | psql redash
Set a new password of your choosing for the ‘redash_reader’ user (since the new installation generated a random password).
psql -c "ALTER ROLE redash_reader WITH PASSWORD 'yourpasswordgoeshere';"
Note: Then you must navigate to the ‘Redash metadata’ data source (/data_sources/1) in the new Redash installation and change the password to match the one entered above.

Grant permissions on the redash database to the redash_reader user.
psql -c "grant select(id,name,type) ON data_sources to redash_reader;" redash
psql -c "grant select(id,name) ON users to redash_reader;" redash
psql -c "grant select on events, queries, dashboards, widgets, visualizations, query_results to redash_reader;" redash
Create a new query in redash (using Redash metadata as the data source) to test that everything is working as expected.