# MySQL

Configure

```bash
sudo mysql_secure_installation utility
```

Unbind localhost only, comment out bind-address = 127.0.0.1

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
sudo systemctl restart mysql
```

Start/create

```sql
CREATE USER '{user}'@'localhost' IDENTIFIED BY '{password}';
CREATE DATABASE {database};
GRANT ALL PRIVILEGES ON {database}.* TO '{user}'@'%' IDENTIFIED BY '{password}' WITH GRANT OPTION;
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

Restore single

```bash
mysql -h {host} -u {user} -p {database} < {filename}
```
