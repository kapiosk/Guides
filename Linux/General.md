# Raspberry Dev

## Permissions

All for owner, group, other

```bash
chmod 777 foldername
```

Make executable for all

```bash
chmod a+x filename
```

Change ownership and give full permissions to owner & group

```bash
chown -R www-data ./
chmod -R 770 ./
```

Turn superuser

```bash
sudo -i
```

### Change mount permissions

Find user

```bash
more /etc/passwd
```

Find group

```bash
/etc/group
```

Edit fstab

```bash
nano /etc/fstab
```

Add/Edit appropriate

```bash
uid=1001,gid=33,
```

## Backup

```bash
sudo dd bs=4M if=/dev/mmcblk0p2 | gzip > raspbian.img.gz
```

For more information, see <https://www.raspberrypi.org/documentation/linux/filesystem/backup.md/>

## Remote SSH/SCP

Create key

```bash
ssh-keygen -t rsa
```

Transfer key to remote server

```bash
scp id_rsa.pub al@pluto.example.com:./
```

Add public key to authorised

```bash
mv id_rsa.pub .ssh/authorized_keys
```

## Remote commands through SSH

```bash
ssh -t username@host 'htop'
```

## Cron

```bash
crontab -e
```

Add your line (Sample runs every hour)

```bash
0 * * * * /usr/bin/python3 /home/pi/test.py >/dev/null 2>&1
```

Check cron status/start/stop

```bash
/etc/init.d/cron status
```

## Rsync

Recursive & preserve, zip, progress

```bash
rsync -azP ~/dir1 username@remote_host:destination_directory
```
