> [@fourtimes](https://github.com/fourtimes) Can you prepare the backup and restore script

## Backup script for postgreSQL
```sh
#!/bin/bash

# Variables
DB_NAME="your_database_name"   # The name of the database to backup
DB_USER="your_username"        # PostgreSQL user
BACKUP_PATH="/path/to/backup"  # Where you want to store the backup
DATE=$(date +"%Y%m%d%H%M%S")   # Timestamp for the backup file

# Backup file name
BACKUP_FILE="$BACKUP_PATH/$DB_NAME-$DATE.sql"

# Create a backup
echo "Starting backup of database: $DB_NAME"
pg_dump -U $DB_USER -F c -b -v -f $BACKUP_FILE $DB_NAME

if [ $? -eq 0 ]; then
    echo "Backup successful! File: $BACKUP_FILE"
else
    echo "Backup failed!"
fi

```
## Restore script for postgreSQL
```sh
#!/bin/bash

# Variables
DB_NAME="your_database_name"                           # The name of the database to restore
DB_USER="your_username"                                # PostgreSQL user
BACKUP_FILE="/path/to/backup/your_backup_file.sql"     # Backup file

# Drop and recreate the database (optional)
echo "Dropping and recreating the database: $DB_NAME"
psql -U $DB_USER -c "DROP DATABASE IF EXISTS $DB_NAME;"
psql -U $DB_USER -c "CREATE DATABASE $DB_NAME;"

# Restore the backup
echo "Restoring database: $DB_NAME from backup: $BACKUP_FILE"
pg_restore -U $DB_USER -d $DB_NAME -v $BACKUP_FILE

if [ $? -eq 0 ]; then
    echo "Restore successful!"
else
    echo "Restore failed!"
fi
```
