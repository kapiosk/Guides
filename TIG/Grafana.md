# Install Grafana on Ubuntu 1804

Add the grafana key and repository

```bash
sudo curl https://packagecloud.io/gpg.key | sudo apt-key add -
echo 'deb https://packagecloud.io/grafana/stable/debian/ stretch main' > /etc/apt/sources.list.d/grafana.list
```

Update the repository and install the grafana package using the apt command below.

```bash
sudo apt update
sudo apt install grafana -y
```

After the installation is complete, start the grafana service and enable it to launch everytime at system boot.

```bash
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

The grafana-server is up and running on default port '3000', check it using netstat.

```bash
netstat -plntu
```
