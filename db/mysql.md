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

Changer le type de données d'une colonne

`$ ALTER TABLE tablename MODIFY columnname INTEGER;`

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


  


