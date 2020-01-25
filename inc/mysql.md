# MySQL Command
## Install (on Ubuntu)
```bash
sudo apt-get install -y mysql-server
```
## Connexion
```bash
mysql -h localhost -u root -p
```
OR
```bash
mysql -u root -p
```

## Create a user
```mysql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```
```mysql
GRANT [type_of_permission] ON [database_name].[table_name] TO 'username'@'localhost';
```
```mysql
GRANT ALL PRIVILEGES ON [database_name].[table_name] TO 'username'@'localhost' IDENTIFIED BY 'password';
```

## Database
### Create
```mysql
CREATE DATABASE [dbname];
```
### Use
```mysql
USE [dbname];
```

## Save
To backup all databases :
```bash
mysqldump --user=[username] --password=[password] --all-databases > [filename].sql
```
To backup one database :
```bash
mysqldump --user=[username] --password=[password] --databases [database] > [filename].sql
```
To back up multiple databases:
```bash
mysqldump --user=[username] --password=[password] --databases [database_1] [database_2] > [filename].sql
```
To save a specific table:
```bash
mysqldump --user=[username] --password=[password] --databases [database] --tables [tableName] > [filename].sql
```
To save several tables:
```bash
mysqldump --user=[username] --password=[password] --databases [database] --tables [tableName_1] [tableName_2] > [filename].sql
```

## Import
```bash
mysql --user=[username] --password=[password] [database] < [filename].sql
```
