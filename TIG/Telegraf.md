# How to install Telegraf Agent on Ubuntu 1804

Install the telegraf package

```bash
sudo apt install telegraf -y
```

After the installation is complete, start the telegraf service and enable it to launch every time at system startup.

```bash
sudo systemctl start telegraf
sudo systemctl enable telegraf
```

The telegraf agent should be up and running, check it using the command below.

```bash
sudo systemctl status telegraf
```

## Configuration

Go to the '/etc/telegraf' directory and rename the default configuration file

```bash
cd /etc/telegraf/
mv telegraf.conf telegraf.conf.default
```

Now create a new other configuration 'telegraf.conf'

```bash
sudo nano telegraf.conf
```

## Sample configuration for Linux Client

```plaintext
# Global Agent Configuration
[agent]
  hostname = "<hostname>"
  flush_interval = "15s"
  interval = "15s"


# Input Plugins
[[inputs.cpu]]
    percpu = true
    totalcpu = true
    collect_cpu_time = false
    report_active = false
[[inputs.disk]]
    ignore_fs = ["tmpfs", "devtmpfs", "devfs"]
[[inputs.io]]
[[inputs.mem]]
[[inputs.net]]
[[inputs.system]]
[[inputs.swap]]
[[inputs.netstat]]
[[inputs.processes]]
[[inputs.kernel]]

# Output Plugin InfluxDB
[[outputs.influxdb]]
  database = "<database>"
  urls = [ "<URL or IP>:8086" ]
  username = "<username>"
  password = "<password>"
  ```

Save and exit.

Telegraf provides telegraf command to manage the configuration, including generate the configuration itself, run the command as below.

```bash
telegraf config -input-filter cpu:mem:disk:swap:system -output-filter influxdb > telegraf.conf
cat telegraf.conf
```

Restart the telegraf service and make sure there is no error.

```bash
sudo systemctl restart telegraf
```

Now test the telegraf settings using the command below.

```bash
sudo telegraf -test -config /etc/telegraf/telegraf.conf --input-filter cpu
sudo telegraf -test -config /etc/telegraf/telegraf.conf --input-filter net
sudo telegraf -test -config /etc/telegraf/telegraf.conf --input-filter mem
```
