Installing infinitude on OrangePi Zero
http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-Zero-2.html

Using a usb rs485 adapter

Use the Ubuntu image...
I initiaaly did desktop, but then tried the server image
Orangepizero2_3.0.6_ubuntu_jammy_server_linux5.16.17.7z

The Orange Pi OS did not work - wifi did not work.

Image a card
boot to it
connect via ethernet ssh (Putty)
use orangepi-config
  set time zone
  enable wifi
  disable ethernet
apt update && apt upgrade && apt autoremove

install Infinitude on OrangePi using Raspberry Pi instructions here:
https://github.com/nebulous/infinitude/wiki/Installing-Infinitude-on-Raspberry-PI-(Raspbian)

create config file /infinitude/infinitude.json 

got some errors when running via command line...
"XMLin() requires either XML::SAX or XML::Parser at ./infinitude line 161"
installed libxml-parser-perl

apt install libxml-parser-perl

set up service...
nano /etc/systemd/system/infinitude.service

enable the service
systemctl enable infinitude

set thermostat proxy to the ip of the orange pi

set infinitude config in home assistant to the ip of the orange pi
