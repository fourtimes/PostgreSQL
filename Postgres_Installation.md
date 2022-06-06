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
