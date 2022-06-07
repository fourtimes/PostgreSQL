### What is PostgreSQL?

- PostgreSQL is an advanced, enterprise-class, and open-source relational database system. PostgreSQL supports both SQL (relational) and JSON (non-relational) querying.

- PostgreSQL is a highly stable database backed by more than 20 years of development by the open-source community.

- PostgreSQL is used as a primary database for many web applications as well as mobile and analytics applications.

---

### PostgreSQL Installation on ubuntu
If you not installed the postgreSQL, use this command,
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```

### Uninstall the postgres 
If you uninstalled the packages, use this command,

```bash
sudo apt-get --purge remove postgresql postgresql-*
sudo apt autoremove
```
### Start the service
```bash
sudo systemctl start postgresql.service
```
### Check the status of the service
```bash
sudo systemctl status postgresql.service
```
### Login into the postgreSQL server
```bash
sudo -u postgres psql
```
**Check the version of psql**
```bash
SELECT version();
```
|db_name|Table_name|
|-------|----------|
|demo|users|
|demo|photos|
|demo|comments|
