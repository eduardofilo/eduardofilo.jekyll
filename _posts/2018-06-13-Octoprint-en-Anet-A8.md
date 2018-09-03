---
layout: post
title: "Octoprint en Anet A8"
date: 2018-06-13 22:40:00
published: false
---

# Octoprint en Anet A8

Siguiendo [esta guía](https://discourse.octoprint.org/t/setting-up-octoprint-on-a-raspberry-pi-running-raspbian/2337).

2018-03-10 21:34:53,951 - serial.log is currently not enabled, you can enable it via Settings > Serial Connection > Log communication to serial.log

G28


start
Info:Brown out Reset
Info: 0.000000 0.000000 0.000000 0.000000 0.000000 0.000000 0.000000 0.000000 0.000000
Free RAM:12337
wait
wait


# Disable BT
https://www.abelectronics.co.uk/kb/article/1035/raspberry-pi-3-and-zero-w-serial-port-usage



# Instalación plugin M84 Motors Off
# https://plugins.octoprint.org/plugins/m84motoff/
cd ~/OctoPrint
./venv/bin/pip install "https://github.com/ntoff/Octoprint-M84MotOff/archive/master.zip"

# G-code
http://marlinfw.org/meta/gcode/

# Apps
https://play.google.com/store/apps/details?id=com.kabacon.octoremote
https://play.google.com/store/apps/details?id=fr.yochi76.printoid.phones.trial

# Plugins intalados:
M84 Motors Off
TouchUI
