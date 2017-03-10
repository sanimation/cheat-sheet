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

## Taille d'une base de donnée

```
SELECT table_schema "DB Name", 
    Round(Sum(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB" 
FROM   information_schema.tables
GROUP  BY table_schema;
``` 

