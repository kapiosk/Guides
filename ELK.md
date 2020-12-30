# ELK Stack

## Installation

Add sources

```bash
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```

Install Elasticsearch

```bash
sudo apt update
sudo apt install elasticsearch
```

Edit Elasticsearch config

```bash
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Change binding and enable single instance mode

```bash
network.host: 0.0.0.0
discovery.type: single-node 
```

Start daemon

```bash
sudo systemctl start elasticsearch
sudo systemctl enable elasticsearch
```

Install Kibana

```bash
sudo apt install kibana
```

Edit Kibana config

```bash
sudo nano /etc/kibana/kibana.yml
```

Start daemon

```bash
sudo systemctl enable kibana
sudo systemctl start kibana
```
