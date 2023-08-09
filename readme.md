Installing infinitude on OrangePi Zero

Using a usb rs485 adapter

http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-Zero-2.html

Use the Ubuntu image...
Orangepizero2_3.0.6_ubuntu_jammy_desktop_xfce_linux5.16.17.7z
(the server image might work better as I never use local interface)

The Orange Pi OS did not work - wifi did not work.

Image a card
boot to it
connect via ethernet ssh (Putty)
use orangepi-config
  enable wifi
  disable ethernet
apt update
apt upgrade

install Infinitude using instructions here:
https://github.com/nebulous/infinitude/

create config file /infinitude/infinitude.json with the following:
{"app_secret":"Pogotudinal","pass_reqs":300,"serial_tty":"\/dev\/ttyUSB0"}

got some errors when running via command line...
"XMLin() requires either XML::SAX or XML::Parser at ./infinitude line 161"
installed libxml-parser-perl

also did 
chmod 777 /dev/ttyUSB0
not sure if needed though

set up service...
nano /etc/systemd/system/infinitude.service
with this content:

[Unit]
Description=Infinitude HVAC control
After=network-online.target

[Service]
LogLevelMax=6
Type=simple
WorkingDirectory=/root/infinitude
ExecStartPre=stty -F /dev/ttyUSB0 38400 cs8 -cstopb -parity -brkint -icrnl -imaxbel -opost -isig -iexten -echo -icanon min 1
ExecReload=stty -F /dev/ttyUSB0 38400 cs8 -cstopb -parity -brkint -icrnl -imaxbel -opost -isig -iexten -echo -icanon min 1
ExecStart=/root/infinitude/infinitude daemon -m production -l http://192.168.1.6:80
Restart=always

[Install]
WantedBy=multi-user.target


enable the service
systemctl enable infinitude

