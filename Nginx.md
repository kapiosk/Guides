# Nginx Stack

## Reverse Proxy

Create Page

```bash
sudo nano /etc/nginx/sites-available/example.com
```

Make simple config

```nginx
server {
	listen 80;
	listen [::]:80;
	server_name example.com;
    #client_max_body_size 300M;
	location / {
        # Set proxy headers
        #proxy_set_header Host $host;
        #proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        #proxy_set_header X-Forwarded-Proto $scheme;

        # These are important to support WebSockets
        #proxy_set_header Upgrade $http_upgrade; #proxy_cache_bypass $http_upgrade;
        #proxy_set_header Connection "Upgrade";

		proxy_pass http://localhost:5601;
        #proxy_http_version 1.1;        
	}
}
```

Link & restart

```bash
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/example.com

sudo service nginx restart
sudo certbot --nginx
```
