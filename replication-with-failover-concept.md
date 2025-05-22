
# PostgeSQL Replication for ubuntu 22

## Environment
- **OS**: Ubuntu 22.04
- **PostgreSQL Version**: 14
- **Nodes**:
  - Master: 10.106.0.1
  - Slave-1: 10.106.0.2
  - Slave-2: 10.106.0.3
  
## We need to install both nodes ( master and slave ) 
```cmd
sudo apt update
sudo apt install postgresql postgresql-contrib -y

sudo systemctl start postgresql
sudo systemctl enable postgresql
sudo systemctl status postgresql
```
##  Configure the Master Node:
```sql
sudo -u postgres psql

CREATE ROLE repl_user WITH REPLICATION LOGIN PASSWORD '@123';

\q
```
Change the configuration `sudo nano /etc/postgresql/14/main/postgresql.conf` file
```conf
listen_addresses = '10.106.0.1'
wal_level = logical
wal_log_hints = on
```

sudo vim /etc/postgresql/14/main/pg_hba.conf
```conf
host    replication     repl_user       10.106.0.2/32           md5
```
```bash
sudo systemctl restart postgresql
```
take a backup for psql lib
```
sudo cp -rf /var/lib/postgresql/14/main/ /var/lib/postgresql/14/main.bk
```

##  Configure the Slave Node - 1:
```md
# stop the psql service
sudo systemctl stop postgresql

# remove the psql library
sudo rm -rv /var/lib/postgresql/14/main/

# backup the psql library from master node
sudo pg_basebackup -h 10.106.0.1 -U repl_user -X stream -C -S replica_1 -v -R -W -D /var/lib/postgresql/14/main/
 
# change the owner permission
sudo chown postgres -R /var/lib/postgresql/14/main/

# start the psql service
sudo systemctl start postgresql
```
## Test the PostgreSQL Replication
#### Master node

```sql
sudo -u postgres psql
CREATE DATABASE test_db;

\c test_db;

CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR (50)
);

INSERT INTO products(product_name) VALUES ('LEATHER JACKET');
INSERT INTO products(product_name) VALUES ('WINTER HOODIE');
INSERT INTO products(product_name) VALUES ('BROWN WALLET');
```

#### Slave node - 1
```sql
sudo -u postgres psql

\c test_db;

SELECT * FROM products;

INSERT INTO products(product_name) VALUES ('RED TSHIRT');   -- ERROR:  cannot execute INSERT in a read-only transaction
```

# Adding and Configure another Slave:

<!-- Add another Slave configuration to the master node.  -->

1. sudo vim `/etc/postgresql/14/main/pg_hba.conf`
```conf
host    replication     repl_user       10.106.0.3/32           md5
```
2. This steps should be followd in Slave-node-2.
```md
# stop the psql service
sudo systemctl stop postgresql

# remove the psql library
sudo rm -rv /var/lib/postgresql/14/main/

# backup the psql library from master node
sudo pg_basebackup -h 10.106.0.1 -U repl_user -X stream -C -S replica_1 -v -R -W -D /var/lib/postgresql/14/main/
                                    # The slot name (replica_2) must be changed when backing up a new Slave node.

# change the owner permission
sudo chown postgres -R /var/lib/postgresql/14/main/

# start the psql service
sudo systemctl start postgresql
```

# step-by-step failover process to switch PostgreSQL roles between Master (Primary) → Slave (Standby) and Slave → Master in Ubuntu 22.04.

## Step 1: Verify Current Roles

Before switching, confirm which server is Master and which is Slave:
On Both Servers:
```bash
sudo -u postgres psql -c "SELECT pg_is_in_recovery();"

# f (false) → Master (Primary)
# t (true) → Slave (Standby)
```

### On Master (Primary):
```bash

sudo -u postgres psql -c "SELECT client_addr, state, sync_state FROM pg_stat_Replication;"
```
This shows connected Slaves.

### On Slave (Standby):
```bash
sudo -u postgres psql -c "SELECT status, sender_host FROM pg_stat_wal_receiver;"
```
This confirms it's receiving WAL logs from the Master.

## Step 2: Promote Slave to Master

#### On the Slave (to be promoted to Master):
```bash
# Promote the standby to primary
sudo -u postgres pg_ctlcluster 14 main promote  # Replace "14" with your PostgreSQL version

# Verify promotion
sudo -u postgres psql -c "SELECT pg_is_in_recovery();"  # Should return `f` (false)
```

## Step 3: Convert Old Master to Slave

1. Stop PostgreSQL
```bash
sudo systemctl stop postgresql
```
2. Clear old data (optional, but recommended)
```bash
sudo -u postgres rm -rf /var/lib/postgresql/14/main/*
```
3. Take a fresh base backup from the new Master
```bash
sudo -u postgres pg_basebackup -h 10.106.0.2 -D /var/lib/postgresql/14/main -U repl_user -P -v -R -X stream -C -S replica_1

```
4. Configure Replication settings
Edit `postgresql.auto.conf` (PostgreSQL 12+):
```bash
sudo -u postgres vim /var/lib/postgresql/14/main/postgresql.auto.conf
```
Add:
```ini
primary_conninfo = 'host=10.106.0.2 port=5432 user=repl_user password=@123'
primary_slot_name = 'replica_1'
```
5. Start PostgreSQL
```bash
sudo systemctl start postgresql
```
6. Verify Replication
```bash
sudo -u postgres psql -c "SELECT status, sender_host FROM pg_stat_wal_receiver;"
```
## Step 5: Verify Failover
### On New Master:
```bash
sudo -u postgres psql -c "SELECT pg_is_in_recovery();"  # Should return `f` (false)
sudo -u postgres psql -c "SELECT * FROM pg_stat_Replication;"  # Should show the old Master as a Slave
```
### On New Slave (Old Master):
```bash
sudo -u postgres psql -c "SELECT pg_is_in_recovery();"  # Should return `t` (true)
sudo -u postgres psql -c "SELECT status FROM pg_stat_wal_receiver;"  # Should show "streaming"
```

#### Troubleshooting
Replication not working? Check logs:
```bash
sudo tail -n 50 /var/log/postgresql/postgresql-14-main.log
```

## Test the configuration

#### Master node

```sql
sudo -u postgres psql

\c test_db;

INSERT INTO products(product_name) VALUES ('LEATHER JACKET');
INSERT INTO products(product_name) VALUES ('WINTER HOODIE');
INSERT INTO products(product_name) VALUES ('BROWN WALLET');
```

#### Slave node
```sql
sudo -u postgres psql

\c test_db;

SELECT * FROM products;

INSERT INTO products(product_name) VALUES ('RED TSHIRT');   -- ERROR:  cannot execute INSERT in a read-only transaction
```


