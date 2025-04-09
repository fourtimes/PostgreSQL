## Installing, Configuring, and Managing PostgreSQL on Ubuntu 22.04

Installing PostgreSQL
```cmd
sudo apt update && sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql && sudo systemctl enable postgresql && sudo systemctl status postgresql
psql --version
```
Switch to the PostgreSQL User
```cmd
sudo -i -u postgres
psql

# Set the password for the postgres user 
ALTER USER postgres PASSWORD 'new_password';

\q
```
  ###  PostgreSQL Configuration Files
```md
# sudo nano /etc/postgresql/14/main/postgresql.conf

listen_addresses = 'localhost'  # change to '*' for all interfaces
port = 5432
```
 Client Authentication Configuration:
```md
# sudo nano /etc/postgresql/14/main/pg_hba.conf
host    all             all             0.0.0.0/0               md5
```
Restart the psql service
```cmd
sudo systemctl restart postgresql
```
### Managing PostgreSQL
```md
# Login as a PostgreSQL user
sudo -u postgres psql

# List all databases:
\l

# List all users:
\du

# List specific db table
\dt

# Create a new database:
CREATE DATABASE db_name;

# Grant privileges to a user on a database
GRANT ALL PRIVILEGES ON DATABASE db_name TO user_name;

# Drop a database
DROP DATABASE db_name;
```

Backing Up and Restoring Databases
```md
# Backup a database using pg_dump
sudo pg_dump db_name > db_backup.sql

# Restore a database from a backup
psql db_name < db_backup.sql
```
