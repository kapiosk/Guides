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
