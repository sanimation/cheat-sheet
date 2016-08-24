# MongoDB

`brew services start mongodb`

Or, if you don't want\/need a background service

`mongod --config /usr/local/etc/mongod.conf`

Import

mongoimport --host localhost --port 27017 --db numeriic --collection terrains --type csv --file \/Users\/sandrinezecler\/Downloads\/tmp.csv --headerline

