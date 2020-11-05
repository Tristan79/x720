# Rasberry Pi suptronics/geekworm x720/x725 Hat (x700/x705/x725/x730/x735/x750/Maxim MAX17043) #
 
In this episode... we will enter the exciting world of...

 * Battery monitor, view status and/or send it to Domoticz or MQTT (Maxim MAX17043)
 * Battery monitor can be used with any generic Maxim MAX17043 (and probably MAX17044) connected to i2c
 * Safe shutdown workaround in software to bypass incorrect capacity reading
 * Setting up properly the cheap real time clock (DS1307)
 * Review of product
 * Why power management of the hat using GPIO can not be used
 * Bonding two network cards 
 
## __WARNING: DO NOT BUY THIS__ ## 

## __WARNING: WHERE IS THE EXTRA LAN ADAPTER GONE??? WELL YOU REBOOTED... AND NOW ITS GONE, YES IT WILL NOT SURVIVE A REBOOT, YOU NEED TO POWER OFF AND REMOVE THE POWER CABLE... SO WHAT IS THE PROBLEM, THE SHORT CABLE TWISTED AND BAD DESIGN__ ## 

## __WARNING: YOU HAVE A X725 AND IT JUST HALTS YOUR PI, LOOKING LIKE IT'S A POWER PROBLEM... NO, NO, NO... YOU HAVE TO UPDATE YOUR PI (APT_GET UPDATE) WITHOUT THE HAT TO THE LATEST VERSION, SEEMS X725 IS BROKEN IN PREVIOUS RELEASES...__ ## 


## __WARNING: THE X725 HAT HAS THE SAME PROBLEMS!!!!__ ## 

## __WARNING: LEAVING THE BATTERIES IN WHILE UNPLUGGED FROM POWER WILL DAMAGE YOUR HAT AFTER A WHILE (COUPLE OF WEEKS WILL DO IT)...__ ## 

## __WARNING: CUTTING THE MAIN POWER TO THE HAT CAN DAMAGE YOUR HAT AND YOUR PI IF BATTERIES ARE INSTALLED!!! NEVER PULL THE ADAPTER FROM THE AC. AT LEAST WITH TESTING, PULL THE PLUG AT THE PI END!!!__ ## 

## __Yeah... this hat is that bad! :( A waste of money... __ ##

## __You bought it just to be able to do that...__ ##

## __And now I am warning you NOT to do that...__ ##

Well I am not amused either...

Problems *and I mean big problems at the hardware and software levels* of the x720 overlaps with suptronics x700, x705, x725, x730, x735 (v2) and x750. Who is provided with the same software and highly probable the same hardware design... 

### see cons/*pros(?)* review below ###

You can modify/use this for any generic Maxim MAX17043 using the i2c bus.

### ToDo ###
 * Shutting down the hat when you call shutdown (sudo halt) (use gpio 18 and add it to /etc/rc0? as the final and last command)
 * Other power mangement GPIO stuff (what does GPIO 17 do?)
 * Rant! (upvote in issues for youtube rant :-)
 * WOL...

### Review of x720 ###

I fill in my full rant here later! 

That will be, uhm, yeah... terrible,... is a word what does not cover this... and I will fully eleborate and explain the cons and pros (listed below)

Parts used
 * 2x suptronic x720 hats (yeah, I have two...)
 * 2x suptronic x720 cases
 * 2x raspberry Pi 3B (v1.2)
 * 4x brand new 18650B Panasonic batteries without protection
 * 2x geekworm 4A power adapters

It is not only the hardware... but you came here because the software accompanied is as bad as the hardware...
Problems occur on both hats, so it is NOT a randomly defective hardware problem. 

Only buy this if considered the pros and cons, and you are going to use the workarounds. And have almost no power outages. Like one in every 5 years :(.  __*YOU HAVE BEEN WARNED*__

#### Cons ####

##### HAT #####
 * Mayor power spikes on GPIO pins when cutting main power. That makes the extension board with the 40 pins break out of the case, quite useless if you use the batteries) Do not bother using that...
 * Undervoltage detected when cutting the main power
 * Top button, which uses GPIO, is triggered when cutting the main power. That also probably means spikes on all other electronics when switching from wired power to battery (and back)... 
 * Previous con makes the top button for reboot or save shutdown useless! You can still use it as a power on button, or for total power down. But make sure you run *sudo halt* first so to not damage your sd card before you do that. 
 * If the shutdown problem occurs when removing the power plug, your board is toast/fried/kaput!!!! (geekworm you lying bastards!!! see https://www.youtube.com/watch?v=enWHudsFcuw)... With fully charged batteries and no power plug inserted. If it will *NOT TURN ON* when pressing the top button, you know you are screwed.
 * The button script will cause reboots when power is lost (related to gpio is triggered when...)
 * Jumper for auto shutdown is 3v DC (according to their specs). But battery meter is so bad it will power off (not safe shutdown) at values lower then ~3.15v high, which is much higher then 3v. Making the jumper useless. DO NOT SET JUMPER
 * Network card can dissapear from your system completely, needing a power unplug and removal of the batteries and thus opening the case, unscrewing 10 screws... whenever that happens
 * Provided little usb cable is reaaaly flimsy and does sometimes stops working. This is not related to network card disappearing thou
 * Battery meter is shit... I mean really shit... up to 112% when fully charged. And if it reaches 0% it will still run for more then an hour... __yeah that shitty__
 * Button for reboot or safe shutdown does not work without batteries present. Their specs say otherwise, but it does not work... The GPIO for the button does NOT work without batteries
 * Makes very, very high pitch sound with no batteries (alas poor dogs & cats... and think of your little children which have still good ears)
 * RTC Time is reset due to bad design... (luckily I am running an NTP server using a usb GPS stick on the same pi)
 * Sometimes make strange noise when cutting the main power
 * Software provided is bad...  really really bad...
 * Support from either geekworm or suptronics is total crap (geekworm... removing my comments on your youtube videos... really... stop lying to your customers...)
 * When batteries are present and it is completely powered off (hold button for more then 8 to 10 seconds) inserting an usb device or network cable in either ports, lights up/flickers the led on top of the case... you should probably never insert a HDMI cable or sound with the batteries already installed...
 * Had to implement my own software
 
##### Case #####
 * No real wall mount holes in case
 * Case Pi micro usb has a big X with a circle... instead of closing it up (Bad design. Intentionally? Why leave it open, if you know it will damage the whole system???) 
 * Case seals up the 5v output from the hat. Why is that closed and not the Pi micro usb?
 * Case feels static, or more probably, the 5v is leaking to the case and I have become ground
 * Top button does not fit properly in the case (of one of the cases)
  
#### Pros ####
 * If it works it works for more then 8 hours on batteries... (but so does a powerbank) *but* you can use the battery monitor workaround to save shutdown making it somewhat an ups... almost... almost...
 * Can use network bonding to double network speed (tested with speedtest-cli on a pi)
 * Like the design of the case (when I am not touching it see last con)

##### Conclusion ####
Do not buy this unless you known what you are doing and have considered the pros, cons and workarounds. 

### So what... I already bought one... get on with it... ###

Tested on...
Buster (july 2019)

#### Make e-vironment great again! ####

Make sure i2c is enabled with raspi-config.

Download the packages needed for running:
```
sudo apt-get install python3-pip i2c-tools
sudo pip3 install smbus
sudo pip3 install paho-mqtt
```

### Tick, Tack ###

Setup the real time clock (DS3107):

sudo nano /boot/config.txt

```
dtoverlay=i2c-rtc,ds1307
```

Remove fake hardware clock
```
sudo systemctl disable fake-hwclock
```

In /lib/udev/hwclock-set put # in front of these lines and the 2 lines containing --systz

```
if [-e /run/systemd/system ]; then
exit
fi
```

Reboot and test with

```
sudo hwclock -d
timedatectl status
```

### Software Battery Monitor ###
Run the battery monitor *(I probably should have called it maxim17043battery.py or something equivalent)*

```
./x720battery.py
```

or 

```
/home/pi/x720/x720battery.py
```

Make the battery monitor and auto shutdown feature run (every minute) by editing crontab with the command:

```
sudo nano /etc/crontab
```

Add the line

```
* * * * * root /home/pi/x720/x720battery.py
```

Create battery monitor configuration file x720battery.conf. Use the included example configuration file as base.

##### Save shutdown #####
Since the jumper for save shutdown and the original software provided is total $#!T, workaround. Use the voltage readout to safely shutdown and calculate the battery percentage. You can adjust the values in the configuration file. And you can monitor the values with MQTT or Domoticz. Your values may different depending on your batteries.

##### Domoticz #####
If you use domoticz: Create a Voltage, Text and two Percentage devices with the domoticzs dummy hardware. Look up their idx's and edit the x720battery.conf file. And make sure you enable it.

##### MQTT #####
If you use MQTT:
edit the x720battery.conf file. And make sure you enable it.

### Very Optional Features ###

#### GPIO ####

See the legacy folder (please do not use)

##### GPIO IN 4 #####
Button pressed. If pressed it will be none zero value. You have to time the button pressed to determine if you want to reboot or shutdown (or maybe do something else).
Unplugging the power will result in triggering this GPIO pin (due to spikes from unplugging) and thus rebooting... so DO NOT USE the legacy x720button.sh script (or the original x720pwr.sh script) . It is useless. It will not work in combination with a powerloss. Also note that if you hold the button long enough with will power of the hat and thus the pi... Maybe you can time it beter. Since it will reboot and not shutdown, so removing the reboot will probably work leaving only the shutdown part, but then see next GPIO... How will you trigger, the GPIO 18 as the very last command when shutting down... But you can probably remove the reboot part and replace the shutdown with something else usefull... (will experiment later)

##### GPIO OUT 18 ##### 
Cut power to hat, this will result in immediately power loss to the rasberry pi. This will not result in a save shutdown (because there is no power anymore). Usage: pull to 1 wait some time, pull back to 0. DO NOT USE the original x720shutdown script. It will eventually corrupt your sd card.

Maybe add it to /etc/rc0? Or something equivalent? Executing it as the last command. Please share your thoughts in the issues...

##### GPIO OUT 17 #####
Pull to 1 to do something. No really no idea what it does... probably does something... but yeah... no docs available.

#### Bonding ####
This can also be used with other network cards and other debian installations. No x720 or Pi needed. But because I figured this out with a Pi and with a x720 (total cost: 3 weeks, yeah...), lets share... I probably need to add some more info...
So fast track to bonding...

Reference: https://raspberrypi.stackexchange.com/questions/78787/howto-migrate-from-networking-to-systemd-networkd-with-dynamic-failover

*Did not use but is almost the same: https://raspberrypi.stackexchange.com/revisions/78788/15*

Using two wires as one!

This will be a very short walkthrough of bonding... if you have issues or missing info well post an issue.

I currently use a netgear gs116 which support LAG, which actually is XOR bonding (thanks netgear :( for letting me think I have all the functionallity of LACP but I only got the subset for XOR bonding... netgear just as cheap as their chinese counterparts, only they learned to hide it better... vommit... documentation just as shit... what is it with you hardware sellers. Make a good product instead of manipulating your customers. You do not have to be manipulating, lying, cheating and be greedy to make money. Just make good products that actually works the way how you promised it to work... If you use LACP or XOR bonding do not forget to configure your switch.

You can use FULL LACP or Active Backup... (google is your friend) for the parameters needed.

I switches over to systemd networking instead of /etc/network/interfaces on the Pi. I tried the default option with the /etc/network/interfaces and it will result in connecting to wifi (if configured and available) instead of the bond in 1 out of 10 situations..., Which is behaviour you do not want... Finally found a solution... Systemd networking fix it. Systemd has very very very poor documentation... :-( Like why if I use static and dhcp mixed with systemd the metric (order of network cards) is fucked? And I have to manually set the metric myself... which is a pain in the butt... Anyway all things have good and bad side, not?

Anyway bonding 180mb throughput instead of 90mbit (maybe more on the newer models)

```
sudo nano /etc/resolvconf.conf
```

Add

```
# Set to NO to disable resolvconf from running any subscribers. Defaults to YES.
resolvconf=NO
```

Run to switch over to systemd networking

```
sudo systemctl mask networking.service
sudo systemctl mask dhcpcd.service
sudo mv /etc/network/interfaces /etc/network/interfaces~
sudo systemctl enable systemd-networkd.service
sudo systemctl enable systemd-resolved.service
# for fast prompt on screen when connecting with HDMI
sudo systemctl disable systemd-networkd-wait-online.service
sudo systemctl mask systemd-networkd-wait-online.service
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

##### Optional Wifi #####

```
sudo nano /etc/wpa_supplicant/wpa_supplicant-wlan0.conf
```

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=DE

network={
    ssid="CHANGE"
    proto=RSN
    key_mgmt=WPA-PSK
    pairwise=CCMP TKIP
    group=CCMP TKIP
    psk="CHANGE"
}
```

Run it...

```
sudo chmod 600 /etc/wpa_supplicant/wpa_supplicant-wlan0.conf
sudo systemctl disable wpa_supplicant.service
sudo systemctl enable wpa_supplicant@wlan0.service
```

Configure it...
```
sudo nano /etc/systemd/network/08-wifi.network
```

```
[Match]
Name=wl*

[Network]
# to use static IP (with your settings) toggle commenting the next 5 lines.
#Address=192.168.1.87/24
#Gateway=192.168.1.1
DHCP=yes

[DHCP]
RouteMetric=20
```

##### Ethernet #####
The commented out lines are for Active Backup...

```
sudo nano /etc/systemd/network/12-bond0.netdev
```

```
[NetDev]
Name=bond0
Kind=bond

[Bond]
Mode=balance-xor  
#Mode=active-backup
#PrimaryReselectPolicy=always
TransmitHashPolicy=layer3+4
MIIMonitorSec=1s
```

```
sudo nano /etc/systemd/network/16-bond0-add-eth.network
```

Split these in two files for ActiveBackup, one with PrimarySlave and the other not... (Name=eth0 and eth1 instead of e*)

```
[Match]
Name=e*
[Network]
Bond=bond0
#PrimarySlave=true
```

Very optional!!! If you use ActiveBackup you can add your Wifi if you want to... (failover to wifi if lan cables are pulled)

sudo nano /etc/systemd/network/20-bond0-add-wifi.network

```
[Match]
Name=wl*
[Network]
Bond=bond0
```

I do not use Wifi... and you can not do a bond in bond as on some other OSes :( so...

To continue...

```
sudo nano /etc/systemd/network/24-bond0-up.network
```

```
[Match]
Name=bond0
[Network]
DHCP=yes
#VLAN=bond0.1003

[DHCP]
RouteMetric=10
```

##### VLAN #####

This is very, very, mucho very optional.... If you want a vlan over a bond...

```
sudo nano /etc/systemd/network/25-bond0-vlan1003.netdev
```

```
[NetDev]
Name=bond0.1003
Kind=vlan

[VLAN]
Id=1003
```

Sidenote: The vlan 1003 is the guest network of the Apple Airports I have, which I use as a second (wifi) network running my IOT devices... In my case vlan 1003 had no internet access. Make sure the Airport is in bridge mode... NOT in any other mode...

You can use dhcp from another device on the vlan, but I use the build in DHCP server

```
sudo nano /etc/systemd/network/26-bond0-vlan1003.network
```

```
[Match]
Name=bond0.1003

[Network]
Address=10.0.1.1
DHCPServer=yes
#IPMasquerade=yes

[DHCPServer]
PoolOffset=100
PoolSize=100
EmitDNS=yes
DNS=10.0.0.2
```

If you set IPMasquerade=yes, it will bridge your networks.

##### Optional Clean Up #####
```
sudo apt install deborphan
sudo apt --autoremove purge openresolv -y
sudo apt --autoremove purge ifupdown -y
sudo apt --autoremove purge dhcpcd5 -y
sudo apt --autoremove purge isc-dhcp-client isc-dhcp-common -y
sudo apt --autoremove purge $(deborphan)
sudo apt --autoremove purge $(deborphan) #two times
```

##### Extra usefull command #####

```
cat /proc/net/bonding/bond0 
```

```
sudo apt-get install arp-scan
sudo arp-scan --interface=bond0.1003 --localnet 
sudo apt-get install nmap
sudo nmap -sP 10.0.1.0/24 
sudo netstat -plunt
pip3 install speedtest-cli
speedtest
```

Please try the speedtest (-single parameter) to see throughput is doubled (unless your isp is too slow)

##### Do not bridge mdns #####
```
sudo nano avahi-daemon.conf 
```

```
deny-interfaces=bond0.1003
allow-interfaces=bond0
```
