# Python

Create virtual environment

```bash
python3 -m venv tutorial-env
```

Activate virtual environment

```bash
source tutorial-env/bin/activate
```

Deactivate virtual environment

```bash
deactivate
```

Dump requirements

```bash
pip freeze > requirementsDefault.txt
```

Install requirements

```bash
pip install -r requirementsDefault.txt
```

Sample header

```python
#!/home/test/tutorial-env python3
# -*- coding: utf-8 -*-
```

## Deployment

Service

```bash
sudo nano /etc/systemd/system/simplzpdf.service
```

```bash
[Unit]
Description=Gunicorn instance to serve simplzpdf
After=network.target

[Service]
User=www-data
Group=www-data
WorkingDirectory=/var/www/html/SimplzPDF
Environment="PATH=/var/www/html/SimplzPDF/venv/bin"
ExecStart=/var/www/html/SimplzPDF/venv/bin/gunicorn --workers 3 --bind unix:simplzpdf.sock -m 007 wsgi:app

[Install]
WantedBy=multi-user.target
```

Nginx

```bash
server {
    listen 80;
    server_name simplzpdf.curis.health;
        location / {
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_pass http://unix:/var/www/html/SimplzPDF/simplzpdf.sock;
    }
}
```
