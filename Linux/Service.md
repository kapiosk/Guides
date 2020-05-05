# Creating a systemd service

## Create

```bash
sudo nano /lib/systemd/system/dummy.service
```

## Create the config

```plaintext
[Unit]
Description=Dummy Service
After=multi-user.target
Conflicts=getty@tty1.service

[Service]
WorkingDirectory=/var/www/html/dev/
User=frank
Type=simple
ExecStart=/usr/bin/python3 /usr/bin/dummy_service.py
StandardInput=tty-force

[Install]
WantedBy=multi-user.target
```

## Useful commands

Reload daemon

```bash
sudo systemctl daemon-reload
```

Enable service

```bash
sudo systemctl enable dummy.service
```

Disable service

```bash
sudo systemctl disable dummy.service
```

Start service

```bash
sudo systemctl start dummy.service
```

Stop service

```bash
sudo systemctl stop dummy.service
```

Check service status

```bash
sudo systemctl status dummy.service
```

## Troubleshooting Commands

Run script in background

```bash
nohup python3 /usr/bin/dummy_service.py &
```

Check if script is running

```bash
ps aux | grep dummy_service.py
```

Kill running script

```bash
sudo pkill -f dummy_service.py
```
