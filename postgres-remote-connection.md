> [@fourtimes ](https://github.com/fourtimes) How to access the server from another server

#  Master Server For PSQL
Installing, Configuring, and Managing PostgreSQL
```cmd
sudo apt update && sudo apt install -y postgresql postgresql-contrib
sudo systemctl start postgresql && sudo systemctl enable postgresql && sudo systemctl status postgresql
psql --version
```

Ensure PostgreSQL is Configured for Remote Connections
```md
# sudo nano /etc/postgresql/<version>/main/postgresql.conf

listen_addresses = '*'
port=5432
```
```md
# sudo nano /etc/postgresql/<version>/main/pg_hba.conf

host    all             all             0.0.0.0/0          md5
```
Restart the PostgreSQL Service
```cmd
sudo systemctl restart postgresql
```
Login PostgreSQL DB
```md
# Login to the postgres user
sudo -u postgres psql

# List all databases:
\l

# List all users:
\du

# Create a new database:
CREATE DATABASE erp;

# Create the remote user
CREATE USER ashli WITH PASSWORD 'xxxxxxxxxx';

# Grant privileges:
GRANT ALL PRIVILEGES ON DATABASE erp TO ashli;
```

# Remote Server For PSQL
Installing, Configuring, and Managing PostgreSQL
```cmd
sudo apt update && sudo apt install -y postgresql postgresql-client
sudo systemctl start postgresql && sudo systemctl enable postgresql && sudo systemctl status postgresql
psql --version
```
Start the PostgreSQL Service
```md
sudo systemctl start postgresql
sudo systemctl enable postgresql
sudo systemctl status postgresql
```
Connect from the Client Server
```cmd
sudo psql -h (private-ip-access-server) -U ashli -d erp
```
# OUTPUT
![Image](https://github.com/user-attachments/assets/8cf47986-4b29-4a58-9168-4d7f823064cf)


https://github.com/orgs/rcms-org/projects/3/views/4?pane=issue&itemId=78535418&issue=rcms-org%7Cissues-and-incidents%7C103
