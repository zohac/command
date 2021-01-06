# Postgresql Command
## Install (on Ubuntu)
```bash
sudo apt-get install -y postgresql postgresql-contrib
```

## Version
```bash
psql --version
````

## Set Password
```bash
sudo passwd postgres
```

## Connexion
```bash
sudo -u postgres psql
```

## Create a user
Create a user with no password:
```postgresql
CREATE USER jonathan;
```
Create a user with a password:
```postgresql
CREATE USER davide WITH PASSWORD 'jw8s0F4';
```
Create a user with a password that is valid until the end of 2004. After one second has ticked in 2005, the password is no longer valid.
```postgresql
CREATE USER miriam WITH PASSWORD 'jw8s0F4' VALID UNTIL '2005-01-01';
```
Create an account where the user can create databases:
```postgresql
CREATE USER manuel WITH PASSWORD 'jw8s0F4' CREATEDB;
```

## Database
### Create
To create a new database:
```postgresql
CREATE DATABASE lusiadas;
```
To create a database sales owned by user salesapp with a default tablespace of salesspace:
```postgresql
CREATE DATABASE sales OWNER salesapp TABLESPACE salesspace;
```
To create a database music with a different locale:
```postgresql
CREATE DATABASE music
    LOCALE 'sv_SE.utf8'
    TEMPLATE template0;
```
To create a database music2 with a different locale and a different character set encoding:
```postgresql
CREATE DATABASE music2
    LOCALE 'sv_SE.iso885915'
    ENCODING LATIN9
    TEMPLATE template0;
```
