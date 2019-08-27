# x720
 x720 Tools
 
```
git clone https://github.com/Tristan79/x720.git
```

Make sure i2c is enabled with raspi-config.

Download the packages needed for running:
```
sudo apt-get install python3-pip i2c-tools
pip3 install smbus
pip3 install paho-mqtt
```

Setup the real time clock:
```
sudo sed -i '$ i rtc-ds1307' /etc/modules
sudo sed -i '$ i echo ds1307 0x68 > /sys/class/i2c-adapter/i2c-1/new_device' /etc/rc.local
sudo sed -i '$ i hwclock -s' /etc/rc.local
```

Set up the top button (do not use):
```
#sudo ./x720/x720button.sh
```

Make the battery monitor run (every minute) by editing crontab with the command:
```
sudo crontab -e
```
Add the following line:
```
* * * * * /home/pi/x720/x720battery.py
```

Create battery monitor configuration file x720battery.conf. Use the example configuration file as base.

If you use domoticz: Create a Voltage, Text and Percentage devices with the domoticzs dummy hardware. Look up their idx's and edit the x720battery.conf file. And make sure you enable it.

If you use MQTT:
edit the x720battery.conf file. And make sure you enable it.
