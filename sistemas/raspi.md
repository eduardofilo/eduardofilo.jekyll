---
layout: default
permalink: /sistemas/raspi.html
---

# Raspberry Pi

## Enlaces

* [Gestión usuarios](http://www.raspberrypi.org/documentation/linux/usage/users.md)
* [IP Estática](http://www.electroensaimada.com/ip-estaacutetica.html)
* [Instalación cliente NO-IP](http://www.noip.com/support/knowledgebase/installing-the-linux-dynamic-update-client/)
* [Ultimate Raspberry Pi Configuration Guide](http://www.instructables.com/id/Ultimate-Raspberry-Pi-Configuration-Guide/?ALLSTEPS)
* [GitPi: A Private Git Server on Raspberry Pi](http://www.instructables.com/id/GitPi-A-Private-Git-Server-on-Raspberry-Pi/all/?lang=es)
* [PiKISS para Raspberry Pi](http://misapuntesde.com/post.php?id=409): Un puñado de scripts con menú para hacerte la vida más fácil
* [Java JDK para ARM](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-arm-downloads-2187472.html)
* [Cylon.js para Raspberry Pi](http://cylonjs.com/documentation/platforms/raspberry-pi/)
* [BerryBoot](http://www.berryterminal.com/doku.php/berryboot): Menú de arranque que permite arrancar varios sistemas instalados en la propia SD, en un disco duro/pendrive externo o en un almacenamiento en red (NAS).
* [An A to Z Beginners Guide to Installing RetroPie on a Raspberry Pi](http://supernintendopi.wordpress.com/)
* [How to install Oracle Java 8 in Debian via repository (JDK8)](http://www.webupd8.org/2014/03/how-to-install-oracle-java-8-in-debian.html)
* [Adafruit - Learn Raspberry Pi](https://learn.adafruit.com/category/learn-raspberry-pi)

## Hardware

* [Lista de hardware verificado](http://elinux.org/RPi_VerifiedPeripherals)
* [Quick2Wire](http://Quick2Wire.com)
* [ESP8266 Serial Esp- 01](http://espressif.com/en/products/esp8266/): Módulo Wifi [por 2,25€](http://es.aliexpress.com/item/2PCS-ESP8266-Serial-Esp-01-WIFI-Wireless-Transceiver-Module-Send-Receive-LWIP-AP-STA/32232009463.html?recommendVersion=1) recomendado por [Fernando](https://twitter.com/m_trombone). [Listado de recursos](http://www.xess.com/blog/esp8266-resources/). Tutorial [conexión a Raspi](http://www.extragsm.com/blog/2014/12/03/connect-esp8266-to-raspberry-pi/).
* [TK2050 50W+50W Dual Channel Class T HIFI Stereo Audio Amplifier Board DC12V 24V](http://www.ebay.com/itm/TK2050-50W-50W-Dual-Channel-Class-T-HIFI-Stereo-Audio-Amplifier-Board-DC12V-24V-/181441180570): Recomendado por Fernando Oroquieta.
* [Using a Console Cable](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable?view=all)
* [Adaptador Wifi (RTL8188CUS)](http://www.raspipc.es/public/home/index.php?ver=tienda&accion=verArticulo&idProducto=1079)
* [Adaptador TDT Conceptronic C08-096 (RTL2832)](http://www.amazon.es/Conceptronic-C08-096-receptor-Dvb-T-radio/dp/B003KCKERE)
* [Receptor infrarrojos](https://energenie4u.co.uk/catalogue/category/PiMote)
* [TP4056 DIY 1A Micro USB Li-Ion Battery Charging Board Charger Module](http://www.dx.com/p/tp4056-diy-1a-micro-usb-li-ion-battery-charging-board-charger-module-blue-373990): Cargador de batería.
* [PowerBoost 500 Charger - Rechargeable 5V Lipo USB Boost](http://www.adafruit.com/product/1944): Alimentación ininterrumpida con batería y gestor de carga.
* [UA0053 ADAPTADOR LOGILINK USB 2.0 AUDIO 5.1](http://www.cetronic.es/sqlcommerce/disenos/plantilla1/seccion/producto/DetalleProducto.jsp?idIdioma=&idTienda=93&codProducto=255195038&cPath=1295): Adaptador audio USB.
* [2-Channel 3W PAM8403 Audio Amplifier Board](http://www.dx.com/p/2-channel-3w-pam8403-audio-amplifier-board-red-146300): Amplificador audio 3W.
* [Stereo 2.8W Class D Audio Amplifier - I2C Control AGC](http://www.adafruit.com/product/1712): Amplificador audio 2.8W con control I2C.

## Distribuciones

* [PiMAME](http://pimame.org/): Raspbian con un frontend para lanzar emuladores.
* [Lakka](http://www.lakka.tv/): Lakka is a lightweight Linux distribution that transforms a credit card sized computer into a full blown emulation console.
* [RetroPie](http://blog.petrockblock.com/retropie/)

## Comandos útiles

### Comprobar asignaciones de cliente No-IP

Las asignaciones dejan marca en el log `syslog`:

```bash
edumoreno@raspi-git /var/log $ sudo fgrep noip syslog
Oct 16 12:18:57 raspi-git noip2[2165]: v2.1.9 daemon ended.
Oct 16 12:19:19 raspi-git noip2[2186]: v2.1.9 daemon started with NAT enabled
Oct 16 12:19:35 raspi-git noip2[2186]: eduardofilo.no-ip.biz set to 88.19.216.95
Oct 16 12:53:06 raspi-git noip2[2186]: v2.1.9 daemon ended.
Oct 16 13:15:23 raspi-git noip2[2217]: v2.1.9 daemon started with NAT enabled
Oct 16 13:15:25 raspi-git noip2[2217]: eduardofilo.no-ip.biz was already set to 88.19.216.95.
```

### Upgrade de Raspbian

```bash
$ sudo apt-get update
$ sudo apt-get upgrade -y
```

### Utilidad de configuración

```bash
$ sudo raspi-config
```

### Backup de la SD (comprimiendo al vuelo)

```bash
$ #Backup:
$ sudo dd if=/dev/mmcblk0 bs=2M | gzip -9 - > Rpi_8gb_backup.img.gz
$ #Restauración (comprimido con gzip):
$ gunzip Rpi_8gb_backup.img.gz -c | sudo dd of=/dev/mmcblk0 bs=2M
$ #Restauración (comprimido con xz):
$ xzcat Rpi_8gb_backup.img.xz | sudo dd of=/dev/mmcblk0 bs=2M
$ #Restauración (comprimido con zip):
$ unzip -p Rpi_8gb_backup.zip | sudo dd of=/dev/mmcblk0 bs=2M
```

### Backup de la SD (comprimiendo al vuelo y diviendo en trozos el fichero resultante)

```bash
$ #Backup:
$ sudo dd if=/dev/mmcblk0 bs=2M | gzip -9 - | split --bytes=2G - Rpi_8gb_backup.img.gz.part_
$ #Restauración:
$ cat Rpi_8gb_backup.img.gz.part_* | gunzip -c | sudo dd of=/dev/mmcblk0 bs=2M
```

### Control de progreso durante flasheo

```bash
$ sudo pkill -USR1 -n -x dd
```

Como alternativa se puede instalar el comando `dcfldd` para sustituir a `dd`, con lo que obtendremos una indicación del progreso de la copia. `dcfldd` informa cada 256 bloques escritos por defecto. Para que lo haga con más frecuencia hay que pasarle la opción `statusinterval` de esta forma:

```bash
$ #Backup:
$ sudo dcfldd statusinterval=10 if=/dev/mmcblk0 bs=2M | gzip -9 - > Rpi_8gb_backup.img.gz
```

### Gestión de la SWAP

Para redimensionar la Swap predeterminada (fichero de 100MB en `/var/swap`):

```bash
$ sudo nano /etc/dphys-swapfile
$ sudo dphys-swapfile setup
$ sudo dphys-swapfile swapon
```

Para consultar el estado de la swap:

```bash
$ swapon -s
```

Para dejar de usar swap:

```bash
$ sudo swapoff -a
```

Para activar la swap tal y como está definida en ''/etc/fstab'':

```bash
$ sudo swapon -a
```

Para activar swap con un fichero en concreto:

```bash
$ sudo swapon /var/swap
```

## Pi-top

### Enlaces

* [pi-top-install](https://github.com/rricharz/pi-top-install): Scripts para controlar el hardware del Pi-top (teclas brillo pantalla, power off, etc.) sobre Raspbian oficial.
* [pi-top-battery-status](https://github.com/rricharz/pi-top-battery-status): Muestra el estado de la batería del Pi-top en Raspbian.

## Artículos interesantes de [TheMagPi](http://www.themagpi.com/)

* Librería Python para controlar un puerto USB: Página 14 de #3 de TheMagPi
* Buffer de dispositivos controlados con el GPIO de RPi: Página 19 de #4 de TheMagPi
* Librería wiringPi: Sirve para comandar y leer el GPIO desde bash. Página 14 de #6 de TheMagPi
* Comunicación entre RaspPi y Arduino: Página 4 de #7 de TheMagPi
* Uso de interrupciones para chequear GPIO sin bucles: Página 12 de #7 de TheMagPi
* Librería Nanpy para comunicar RaspPi y Arduino por USB: Página 10 de #8 de TheMagPi
* WebIOPi - Framework REST para controlar el GPIO: Página 8 de #9 de TheMagPi

## Seguridad

### SSH

Editar el fichero `/etc/ssh/sshd_config` y modificar/añadir las siguientes líneas ([fuente](http://blog.zoogon.net/2013/01/protegiendo-un-poco-nuestra-raspberry.html)):

```
PermitRootLogin no
MaxAuthTries 3
MaxStartups 5
AllowUsers edumoreno
```

Medidas de protección:

* [Top 20 OpenSSH Server Best Security Practices](http://www.cyberciti.biz/tips/linux-unix-bsd-openssh-server-best-practices.html)
* [Protege tu servidor casero de ataques externos](http://blog.desdelinux.net/protege-tu-servidor-casero-de-ataques-externos/)
* [Protegiendo el servidor SSH con fail2ban](http://blog.zoogon.net/2015/02/protegiendo-el-servidor-ssh-con-fail2ban.html)

### Varios

* Cambiar contraseña predeterminada de usuario `pi` o mejor eliminar la cuenta.
* Instalar paquete `fail2ban`.
* Desinstalar paquete `wolfram-engine` que ocupa mucho y no se suele usar:
  * `sudo apt-get remove wolfram-engine`
