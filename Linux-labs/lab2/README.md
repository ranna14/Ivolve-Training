
# Lab 2: Automate MySQL Database Backups

## Overview
This Lab automates the process of taking daily backups of a MySQL database at 5:00 PM. The backup script creates a compressed .sql file and deletes backups older than 7 days. The script is scheduled using cron.

## Steps
### Step 1: Install MySQL:
```bash
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql
```
### Step 2: Create the Backup Script
Create a backup script:
```bash
 sudo vim backup.sh
```
```bash
#!/bin/bash 

#database credentials 
USER="root"
PASSWORD="12345"
DATABASE_NAME="mysql"


#database backup
BACKUP_DIR="/home/rana/backup_dir"


#backupfile with current date
BACKUP_FILE="$BACKUP_DIR/mysql_database-$(date +\%F).sql"

#taking backup usinf mysqldump
mysqldump -u "$USER" -p  "$DATABASE_NAME" > "$BACKUP_FILE"

#check success
if [ $? -eq 0 ]; then
    echo "$(date): Backup succeeded: $BACKUP_FILE" >> /var/log/mysql_backup.log
    gzip "$BACKUP_FILE" 
else
    echo "$(date): Backup failed!" >> /var/log/mysql_backup.log
    exit 1
fi

#delete backups older than 7 days
find "$BACKUP_DIR" -type f -name "*.sql.gz" -mtime +7 -exec rm {} \;
```
### Step 3: Make the Script Executable
```bash
chmod +x backup.sh
```
### Step 4: Schedule with Cron
1-Open the crontab editor:
```bash
crontab -e
```
2-Add the following line to schedule the script to run daily at 5:00 PM:
```bash
0 17 * * * /home/user/backup.sh >> /var/log/mysql_backup.log 2>&1
```
## Verification
### Test the Script Manually:
```bash
./backup.sh
```

