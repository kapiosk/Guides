# Raspberry as WiFi bridge/AP

Ref: <https://www.raspberrypi.org/forums/viewtopic.php?t=193770>

Update and install dependancies

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install hostapd bridge-utils
```

Stop hostapd so we can edit it

```bash
sudo systemctl stop hostapd
```

Create bridge br0.

```bash
sudo brctl addbr br0
```

Create file __/etc/hostapd/hostapd.conf__ and add:

```plaintext
interface=wlan0
bridge=br0
#driver=nl80211
ssid=RPiNet
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=mypassphrase
wpa_key_mgmt=WPA-EAP-SHA256
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

Edit __/etc/default/hostapd__ and uncomment:

```bash
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```

Add eth0 to br0

```bash
sudo brctl addif br0 eth0
```

Edit __/etc/network/interfaces__ and add:

```plaintext
auto br0
iface br0 inet dhcp
bridge_ports eth0 wlan0
```

Edit __/etc/dhcpcd.conf__ and add this above other interfaces:

```plaintext
denyinterfaces eth0 wlan0
```

Reboot

```bash
sudo reboow now
```

## Resolution config

```bash
sudo nano /etc/resolv.conf
```
