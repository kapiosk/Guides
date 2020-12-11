# MySQL

Configure

```bash
sudo mysql_secure_installation utility
```

Start/create

```sql
CREATE USER '{user}'@'localhost' IDENTIFIED BY '{password}';
CREATE DATABASE {database};
GRANT ALL PRIVILEGES ON {database}.* TO '{user}'@'localhost' IDENTIFIED BY '{password}';
FLUSH PRIVILEGES;
```

Client

```bash
sudo apt-get install mysql-client
```

Backup single

```bash
mysqldump -h {url} {database}> {filename}.sql -u {user} -p
```

Backup all

```bash
mysqldump --all-databases --single-transaction --quick --lock-tables=false > full-backup-$(date +%F).sql -h {url} -u {user} -p
```
