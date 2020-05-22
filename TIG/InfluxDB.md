# How to Install InfuxDB Ubuntu 1804

Add the influxdata Key

```bash
sudo curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
```

Add the influxdata repository

```bash
source /etc/lsb-release
echo "deb https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
```

Update Repositories and install

```bash
sudo apt update
sudo apt install influxdb -y
```

After the installation is complete, start the influxdb service and enable it to launch every time at system boot.

```bash
sudo systemctl start influxdb
sudo systemctl enable influxdb
```

Check the opened ports on the system.

```bash
netstat -plntu
```

Make sure you get influxdb ports '8088'and '8086' on the 'LISTEN' state.

## Create InfluxDB Database and User

Run the 'influx' command below.

```bash
influx
```

Create a new database and user

```bash
create database <database>
create user <user> with password '<password>'
```
