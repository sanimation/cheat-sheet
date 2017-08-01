# Connect to Docker MySQL container from localhost?

## Using docker-compose up

Since you published port 3306 on your docker host, from that host itself you would connect to `127.0.0.1:3306`.

## Using docker-compose run

In that case the port mapping section of the docker-compose.yml file is ignored. To have the port mapping section considered, you have to add the --service-ports option:

```
docker-compose run --service-ports db
```

## Additional note

Beware that by default, the mysql client tries to connect using a unix socket when you tell it to connect to localhost. So do use 127.0.0.1 and not localhost:

```
$ mysql -h 127.0.0.1 -P 3306 -u root
```

Welcome to the MySQL monitor. Commands end with ; or \g. Your MySQL connection id is 1 Server version: 5.6.26 MySQL Community Server (GPL)

Copyright (c) 2000, 2015, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its affiliates. Other names may be trademarks of their respective owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>


```
$ mysql -h localhost -P 3306 -u root
```

ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)