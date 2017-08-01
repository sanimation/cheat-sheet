# MySQL

## Mode ligne de commande

`$ mysql -u root -p`

## Changer de mot de passe

`$mysqladmin -u root -p password NEWPASSWORD`

## Lister les bases de données

`$ SHOW DATABASES`

## Changer de base de données

`$ use <dbname>`

## Lister les tables

`$ SHOW TABLES`

## Créer une table

`$ CREATE DATABASE dbname;`

## Changer le type de données d'une colonne

`$ ALTER TABLE tablename MODIFY columnname INTEGER;`


## Taille d'une base de donnée

```
SELECT table_schema "DB Name", 
    Round(Sum(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB" 
FROM   information_schema.tables
GROUP  BY table_schema;
``` 
## Remote access

1 - first check status:

```
netstat -tulpen
```

2 - modify your configuration :

```
 vi /etc/mysql/my.cnf
 bind-address = 0.0.0.0
```

3 - entry mysql to give privileges
 
```
GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'%'IDENTIFIED BY 'mypassword' WITH GRANT OPTION;

FLUSH PRIVILEGES;
```

4 - restart mysql

```
 /etc/init.d/mysql restart

```

## Importer un fichier csv

```
mysqlimport --ignore-lines=1 --fields-terminated-by=, --verbose --local -u [user] -p [database] /path/to/address.csv
```
* `--ignore-lines` will ignore the number of specified lines, in this case we are omiting the first one as it is the header of the table
* `--fields-terminated-by` Will tell the command what character is the delimiter one, a comma in this case.
* `--verbose` Makes the command to be talkie, I always prefer this mode with commands when using them for first time.
* `--local` Tells the command that the CSV file should be read in the local file system of the server.
* `--u [user]` Is the user with rights to write on the database
* `--p` Tells the command to prompt for [user]'s password
[database] The name of the database where the table was created and where the data is going to be inserted
* `/path/to/address.csv` Is the complete path to the csv file, be sure to match the name of the file address in this case, with the name of the table, otherwish it will not work, the extension might be anything or none at all.

## Importer un fichier sql

```
mysql -u username -p database_name < file.sql
```