# What is PostgreSQL
- PostgreSQL is an advanced, enterprise-class, and open-source relational database system. PostgreSQL supports both SQL (relational) and JSON (non-relational) querying.

- PostgreSQL is a highly stable database backed by more than 20 years of development by the open-source community.

- PostgreSQL is used as a primary database for many web applications as well as mobile and analytics applications.
### PostgreSQL Installation on ubuntu

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql.service
sudo systemctl status postgresql.service
```
### Uninstall the postgres 

```bash
sudo apt-get --purge remove postgresql postgresql-*
sudo apt autoremove
```
### Login into the postgreSQL server
```bash
sudo -u postgres psql
```
**Check the version of psql**
```bash
SELECT version();
```
**Create the new user:**
```bash
CREATE USER (your_username) WITH ENCRYPTED PASSWORD ('your_password');
GRANT ALL PRIVILEGES ON DATABASE (your_dbname) TO (your_username);
```
**Remote Backup**
```bash
sudo pg_dump -U (username) -h (host(or)ip a) -p 5432 (database_name) > (foldername)
ex:
----
sudo pg_dump -U ashli -h localhost -p 5432 demo > /home/dodo/Desktop/demoo.sql
```
