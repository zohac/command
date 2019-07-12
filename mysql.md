# MySQL Command
## Install (on Ubuntu)
```bash
sudo apt-get install -y mysql-server
```
## Connexion
```bash
mysql -h localhosy -u root -p
```
OR
```bash
mysql -u root -p
```

## Save
To backup all databases :
```bash
mysqldump --user=username --password=password --all-databases > filename.sql
```
To backup one database :
```bash
mysqldump --user=username --password=password --databases nom_de_la_base > filename.sql
```
To back up multiple databases:
```bash
mysqldump --user=username --password=password --databases database_1 database_2 > filename.sql
```
To save a specific table:
```bash
mysqldump --user=username --password=password --databases nom_de_la_base --tables tableName > filename.sql
```
To save several tables:
```bash
mysqldump --user=username --password=password --databases nom_de_la_base --tables tableName_1 tableName_2 > filename.sql
```
