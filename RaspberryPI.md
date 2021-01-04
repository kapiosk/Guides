# Raspberry PI

## DHT Issue on Pi4

Install dependencies

```bash
pip3 install adafruit-circuitpython-dht
sudo apt-get install libgpiod2
```

Edit Detect File

```bash
sudo nano /home/pi/.local/lib/python3.7/site-packages/Adafruit_DHT/platform_detect.py
```

Add case for Pi4

```bash
elif match.group(1) == 'BCM2711':
        # Pi 4
        return 3
```

## Lost sound on Raspberry OS upgrade

```bash
sudo rm .asoundrc
sudo raspi-config
sudo reboot now
```
