# PostgreSQL Replication -  Master, Slave Node

```md
 Master Node - 172.31.44.242
 Slave Node - 172.31.3.113
```
On Master and Slave servers, PostgreSQL 16 must have be installed following the below command.
```md
sudo apt update
sudo apt install postgresql postgresql-contrib -y
```
### Step1: Configurations on master server
_Change the below configuration for replication process._
```md
# sudo vim /etc/postgresql/16/main/postgresql.conf

listen_addresses = '*'      # '*' - means allowing all the users.
wal_level = logical
wal_log_hints = on
max_wal_senders = 5
```
```md
# sudo vim  /etc/postgresql/16/main/pg_hba.conf

host    replication     all      0.0.0.0/0     md5
```
Now, restart the PostgreSQL on Master server by using below command.
```cmd
sudo systemctl restart postgresql
```
Now, connect to PostgreSQL on Master server and create replica login.
```psql
CREATE USER replicator WITH REPLICATION LOGIN PASSWORD 'xxxxxxx';

\q
```
### Step2: Configurations on slave(standby) server
We have to stop PostgreSQL on Slave server by using following command.
```md
sudo systemctl stop postgresql
```
Take backup of main(data) directory.
```
sudo cp -R /var/lib/postgresql/16/main/ /var/lib/postgresql/16/main_old/
sudo chown postgres -R /var/lib/postgresql/16/main/
```
Now, remove the contents of main(data) directory on slave server.
```cmd
sudo rm -rf /var/lib/postgresql/16/main/
```
Now, use basebackup to take the base backup with the right ownership with postgres(or any user with right permissions).
```cmd
sudo pg_basebackup -h  172.31.44.242 -D /var/lib/postgresql/16/main/ -U replicator -P -v -R -X stream -C -S slaveslot1
```
            Note:
            -------
            1. 172.31.44.242 - master node ip
            2. replicator - master node psql replication user
            3. Then provide the password for user replicator created in master server.

![Image](https://github.com/user-attachments/assets/1d885c7d-e48a-4a93-8025-290f0672b9e8)

 Notice that standby.signal is created and the connection settings are appended to postgresql.auto.conf.
```cmd
sudo ls -ltrh /var/lib/postgresql/16/main/
sudo chown postgres -R /var/lib/postgresql/16/main
```
```
sudo systemctl start postgresql
```
### Test the PostgreSQL Replication
Log in to the PostgreSQL server on the master node.
```cmd
sudo -u postgres psql
```
Create the DB
```cmd
CREATE DATABASE test_db;
```
Then, switch to the new database.
```cmd
 \c test_db;
```
Create a new `products` table under the `test_db` database.
```psql
CREATE TABLE products (
               product_id SERIAL PRIMARY KEY,
               product_name VARCHAR (50)
           );
```
Next, `INSERT` three records in the `products` table.
```psql
INSERT INTO products(product_name) VALUES ('LEATHER JACKET');
INSERT INTO products(product_name) VALUES ('WINTER HOODIE');
INSERT INTO products(product_name) VALUES ('BROWN WALLET');
```
![Image](https://github.com/user-attachments/assets/65c50de6-9ff1-45b9-92c4-66f11917093b)

Now in a new SSH terminal window, connect to the PostgreSQL server on the replica(slave) node as postgres.
```cmd
sudo -u postgres psql
```
Create the DB
```cmd
CREATE DATABASE test_db;
```
Then, switch to the new database.
```cmd
 \c test_db;
```
```psql
SELECT * FROM products;
```
Your replica node is running in hot standby mode and can only accept read-only operations. You may attempt to submit the following INSERT statement in the replica node to check this behavior.
```
test_db=# INSERT INTO products(product_name) VALUES ('RED TSHIRT');
```
Since the replica node can not accept write operations, you should get the following error. However, the same command will succeed in the master node.
```
ERROR:  cannot execute INSERT in a read-only transaction
```
Your PostgreSQL replication setup is now working as expected.

![Image](https://github.com/user-attachments/assets/7a344c6d-b00c-4980-b433-243590cdf012)

