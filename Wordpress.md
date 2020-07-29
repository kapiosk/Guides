# Wordpress

## Discover

Find sql & path credentials by searching for config

```bash
sudo find /var/www/html/ -name wp-config.php
```

## Backup

### MySQL

Backup & compress mysql db of site (note that password does not have space after -p)

```bash
mysqldump -u {user} -p{pass} {dbname} | gzip > {path}/db.sql.gz
```

Or all dbs on MySQL

```bash
mysqldump -u {user} -p{pass} --all-databases | gzip > {path}/mysql.sql.gz
```

### Certificates

Backup let's encrypt certificates (also see install and use certbot for nginx)

```bash
tar -zcvf {path}/certificates.tar.gz /etc/letsencrypt/
```

### Nginx

Backup all nginx configs, note that you need to install nginx, etc before hand. Also take care with php-fpm version.

```bash
tar -zcvf {path}/nginxconfig.tar.gz /etc/nginx/sites-available/
```

Last backup sites

```bash
tar -zcvf {path}/allsite.tar.gz /var/www/html
```

### Restore MySQL

Create and grant access

```sql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'user_password';
CREATE DATABASE [database];
GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'localhost';
```

Restore db

```bash
mysql -u [user] -p [database_name] < [filename].sql
```

### Useful commands

Extract gzip (single file)

```bash
gzip -d db.sql.gz
```

Extract folder

```bash
tar xvzf files.tar.gz
```
