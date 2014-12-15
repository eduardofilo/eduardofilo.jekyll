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

## Distribuciones
* [PiMAME](http://pimame.org/): Raspbian con un frontend para lanzar emuladores.
* [Lakka](http://www.lakka.tv/): Lakka is a lightweight Linux distribution that transforms a credit card sized computer into a full blown emulation console.

## Comandos útiles

### Comprobar asignaciones de cliente No-IP

Las asignaciones dejan marca en el log `syslog`:
{% highlight bash %}
edumoreno@raspi-git /var/log $ sudo fgrep noip syslog
Oct 16 12:18:57 raspi-git noip2[2165]: v2.1.9 daemon ended.
Oct 16 12:19:19 raspi-git noip2[2186]: v2.1.9 daemon started with NAT enabled
Oct 16 12:19:35 raspi-git noip2[2186]: eduardofilo.no-ip.biz set to 88.19.216.95
Oct 16 12:53:06 raspi-git noip2[2186]: v2.1.9 daemon ended.
Oct 16 13:15:23 raspi-git noip2[2217]: v2.1.9 daemon started with NAT enabled
Oct 16 13:15:25 raspi-git noip2[2217]: eduardofilo.no-ip.biz was already set to 88.19.216.95.
{% endhighlight %}

### Upgrade de Raspbian
{% highlight bash %}
$ sudo apt-get update
$ sudo apt-get upgrade -y
{% endhighlight %}

### Utilidad de configuración
{% highlight bash %}
$ sudo raspi-config
{% endhighlight %}

### Backup de la SD (comprimiendo al vuelo)
{% highlight bash %}
#Backup:
$ sudo dd if=/dev/mmcblk0 bs=2M | gzip -9 - > Rpi_8gb_backup.img.gz
#Restauración:
$ gunzip Rpi_8gb_backup.img.gz -c | sudo dd of=/dev/mmcblk0 bs=2M
{% endhighlight %}

### Backup de la SD (comprimiendo al vuelo y diviendo en trozos el fichero resultante)
{% highlight bash %}
#Backup:
$ sudo dd if=/dev/mmcblk0 bs=2M | gzip -9 - | split --bytes=2G - Rpi_8gb_backup.img.gz.part_
#Restauración:
$ cat Rpi_8gb_backup.img.gz.part_* | gunzip -c | sudo dd of=/dev/mmcblk0 bs=2M
{% endhighlight %}

### Gestión de la SWAP
Para redimensionar la Swap predeterminada (fichero de 100MB en `/var/swap`):
{% highlight bash %}
sudo nano /etc/dphys-swapfile
sudo dphys-swapfile setup
sudo dphys-swapfile swapon
{% endhighlight %}

Para consultar el estado de la swap:
{% highlight bash %}
swapon -s
{% endhighlight %}

Para dejar de usar swap:
{% highlight bash %}
sudo swapoff -a
{% endhighlight %}

Para activar la swap tal y como está definida en ''/etc/fstab'':
{% highlight bash %}
sudo swapon -a
{% endhighlight %}

Para activar swap con un fichero en concreto:
{% highlight bash %}
sudo swapon /var/swap
{% endhighlight %}

## Artículos interesantes de TheMagPi
* Librería Python para controlar un puerto USB: Página 14 de #3 de TheMagPi
* Buffer de dispositivos controlados con el GPIO de RPi: Página 19 de #4 de TheMagPi
* Librería wiringPi: Sirve para comandar y leer el GPIO desde bash. Página 14 de #6 de TheMagPi
* Comunicación entre RaspPi y Arduino: Página 4 de #7 de TheMagPi
* Uso de interrupciones para chequear GPIO sin bucles: Página 12 de #7 de TheMagPi
* Librería Nanpy para comunicar RaspPi y Arduino por USB: Página 10 de #8 de TheMagPi
* WebIOPi - Framework REST para controlar el GPIO: Página 8 de #9 de TheMagPi


## Hardware

* [Lista de hardware verificado](http://elinux.org/RPi_VerifiedPeripherals)
* [Quick2Wire](http://Quick2Wire.com)

## Seguridad

### SSH

Editar el fichero `/etc/ssh/sshd_config` y modificar/añadir las siguientes líneas ([fuente](http://cuadernodelviaje.blogspot.com.es/2013/01/protegiendo-un-poco-nuestra-raspberry.html)):

{% highlight text %}
PermitRootLogin no
MaxAuthTries 3
MaxStartups 5
AllowUsers edumoreno
{% endhighlight %}

Medidas de protección:

* [Top 20 OpenSSH Server Best Security Practices](http://www.cyberciti.biz/tips/linux-unix-bsd-openssh-server-best-practices.html)
* [Protege tu servidor casero de ataques externos](http://blog.desdelinux.net/protege-tu-servidor-casero-de-ataques-externos/)

### Varios

* Cambiar contraseña predeterminada de usuario `pi` o mejor eliminar la cuenta.
* Instalar paquete `fail2ban`.