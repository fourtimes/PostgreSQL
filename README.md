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

**Database Details:**
|db_name|Table_name|
|-------|----------|
|demo|users|
|demo|photos|
|demo|comments|

### Login into the postgreSQL server

```bash
sudo -u postgres psql
```

**Check the version of psql**

```bash
SELECT version();
```

**Create the database**

```bash
CREATE DATABASE demo
```

**Enter into the database**

```bash
\c demo
```

**Create the table inside the database**

```bash
CREATE TABLE users (
	id serial PRIMARY KEY,
	username VARCHAR ( 50 ) NOT NULL
);
```

```bash
CREATE TABLE photos (
   id serial PRIMARY KEY,
   photo_name VARCHAR ( 50 ) NOT NULL,
   user_id INTEGER REFERENCES users(id)
);
```

```bash
CREATE TABLE comments (
   id serial PRIMARY KEY,
   content VARCHAR ( 50 ) NOT NULL,
   user_id INTEGER REFERENCES users(id),
   photo_id INTEGER REFERENCES photos(id)
);
```

**Insert the values into 3 tables**

```bash
INSERT INTO users (username) VALUES ('joe'),('vicky'),('mervin'),('joseph'),('johnson'),('ashli');
```

```bash
INSERT INTO photos (photo_name,user_id) VALUES ('nature',2),('rainbow',3),('rainfall',5),('flower',6),('rabbit',1),('elephant',4);
```

```bash
INSERT INTO comments (content,user_id,photo_id) VALUES ('looks so beautiful',2,2),('it is a big bunny',4,1),('rainfall is awesome',5,4);
```

**To view the detailed content in table using SELECT statement**

```bash
SELECT * FROM users;
SELECT * FROM comments;
SELECT * FROM photos;
```

**To view the specified column in table using SELECT statement with WHERE Condidtion**

```bash
SELECT content,user_id FROM comments;
SELECT username FROM users WHERE id=6;
```

**Arithmetic operators**

```bash
SELECT content, user_id + photo_id AS sum_content FROM comments;
SELECT content, user_id * photo_id AS mul_content FROM comments;
```
![image](https://user-images.githubusercontent.com/91359308/172534697-f69f9301-1cf4-4f05-aad6-64476e4cf496.png)
