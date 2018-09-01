---
layout: post
title: "Crankshaft - AndroidAuto sobre Raspberry Pi"
date: 2018-06-13 22:30:00
published: false
---

# Crankshaft - AndroidAuto sobre Raspberry Pi

## Soldando alimentación

https://raspberrypi.stackexchange.com/questions/76653/powering-raspberry-pi-with-broken-micro-usb-connector

## Compras

-Relé: https://es.aliexpress.com/item/12V-30-40-A-Amp-5-Pin-5P-Automotive-Harness-Car-Auto-Relay-Socket-5-Wire/32569903186.html
-Regulador tensión: https://es.aliexpress.com/item/MP1584EN-ultra-small-DC-DC-3A-power-step-down-adjustable-module-Buck-Converter-24V-turn-12v/32382698190.html
-Extractor Radio: https://es.aliexpress.com/item/1-Pair-90mm-Car-Radio-Stereo-Removal-Key-Tool-For-Vauxhall-Opel-Corsa-C-Meriva-PC5/32767508369.html
-Marco: https://es.aliexpress.com/item/Doble-Din-Facia-para-Opel-Astra-Antara-Corsa-Zafira-Radio-DVD-est-reo-CD-Panel-Dash/32849366982.html
-Micrófono: https://es.aliexpress.com/item/Mini-Condenser-Microphone-USB-Lavalier-Microfone-for-Computer-PC-Laptop-etc-with-USB-connector/32805808159.html

## Personalización pantalla de conexión

Hay que poner un fichero PNG con nombre `wallpaper.png` en el directorio `crankshaft` de la partición `boot`. La imagen tiene que tener la misma resolución de la pantalla. En el caso de la pantalla oficial de Raspberry 7" utilizada en este tutorial, la resolución es: 800x480px.

## Ajustes

[Guía](https://drive.google.com/file/d/1plZ0zGBW0fsMs5uB2fiXDqz25OhxYzOo/view)

Los ajustes en forma de fichero de configuración (que corresponden con los que se pueden modificar en modo gráfico) están en el fichero `openauto.ini` dentro del directorio `crankshaft` de la partición `boot`.

## Fuente alimentación

http://www.instructables.com/id/ArduinoMicrocontroller-MOSFET/
http://forum.arduino.cc/index.php?topic=7497.msg59812#msg59812

### Mausberry Circuits Switch

[Car Switch](https://mausberry-circuits.myshopify.com/collections/frontpage/products/3a-car-supply-switch-1)

Crankshaft está basado en Raspbian, así que se puede instalar el script siguiendo las instrucciones correspondientes a este sistema en la sección "Installing the script" de la página [Car Setup](http://mausberrycircuits.com/pages/car-setup).

También se puede instalar manualmente copiando un script en la ruta `/etc/switch.sh`, dándole permisos de ejecución y añadiendo lo siguiente al final del fichero `/etc/rc.local` (justo antes del `exit 0`):

    /etc/switch.sh &

El script es:

```bash
#!/bin/bash

#this is the GPIO pin connected to the lead on switch labeled OUT
GPIOpin1=23

#this is the GPIO pin connected to the lead on switch labeled IN
GPIOpin2=24

#Enter the shutdown delay in minutes
delay=0

echo "$GPIOpin1" > /sys/class/gpio/export
echo "in" > /sys/class/gpio/gpio$GPIOpin1/direction
echo "$GPIOpin2" > /sys/class/gpio/export
echo "out" > /sys/class/gpio/gpio$GPIOpin2/direction
echo "1" > /sys/class/gpio/gpio$GPIOpin2/value
let minute=$delay*60
SD=0
SS=0
SS2=0
while [ 1 = 1 ]; do
power=$(cat /sys/class/gpio/gpio$GPIOpin1/value)
uptime=$(</proc/uptime)
uptime=${uptime%%.*}
current=$uptime
if [ $power = 1 ] && [ $SD = 0 ]
then
SD=1
SS=${uptime%%.*}
fi

if [ $power = 1 ] && [ $SD = 1 ]
then
SS2=${uptime%%.*}
fi

if [ "$((uptime - SS))" -gt "$minute" ] && [ $SD = 1 ] && [ $power = 1 ]
then
poweroff
SD=3
fi

if [ "$((uptime - SS2))" -gt 20 ] && [ $SD = 1 ]
then
SD=0
fi

sleep 1
done
```
