---
layout: post
title: "Raspberry Pi2 + KODI + Tvheadend"
date: 2015-03-14 15:04:00
published: true
---

![KODI Logo](/images/posts/kodi-logo.png)

A continuación se describe el montaje de un media center ejecutándose sobre [Raspberry Pi 2](http://www.raspberrypi.org/raspberry-pi-2-on-sale/) basado en la distribución [OpenELEC](http://openelec.tv/) que implementa de forma muy ligera el software media center [Kodi](http://kodi.tv/) (anteriormente llamado XBMC). Se incorpora un decodificador TDT gestionado con el software [Tvheadend](https://tvheadend.org/).

## Elementos necesarios

Empezamos con la lista de piezas que vamos a necesitar.

### Hardware

* Raspberry Pi 2: En [Raspipc.es](http://www.raspipc.es/public/home/index.php?ver=tienda&accion=verArticulo&idProducto=1210) o en [Cooking-Hacks.com](http://www.cooking-hacks.com/shop/raspberry-pi/raspberry-pi-2-model-b)
* Tarjeta microSD: En [Raspipc.es](http://www.raspipc.es/public/home/index.php?ver=tienda&accion=verArticulo&idProducto=1016) o en [Amazon.es](http://www.amazon.es/Samsung-Evo-MB-MP16DA-EU-adaptador/dp/B00J2BU7WO)
* [Dongle Wifi](http://www.raspipc.es/public/home/index.php?ver=tienda&accion=verArticulo&idProducto=1079)
* Hub USB alimentado: En [Raspipc.es](http://www.raspipc.es/public/home/index.php?ver=tienda&accion=verArticulo&idProducto=1065) o en [Pccomponentes.com](http://www.pccomponentes.com/conceptronic_stylish_hub_4_puertos_usb_2_0_azul.html)
* Sintonizador TDT USB: En [Pccomponentes.com](http://www.pccomponentes.com/conceptronic_sintonizador_tdt_usb.html) o en [Amazon.es](http://www.amazon.es/Conceptronic-C08-096-receptor-Dvb-T-radio/dp/B003KCKERE)
* [Cable HDMI](http://www.raspipc.es/public/home/index.php?ver=tienda&accion=verArticulo&idProducto=1115). Vamos a suponer que el televisor donde se va a instalar posee una entrada HDMI de tamaño estándar. En caso contrario necesitaremos el adaptador correspondiente.

### Software

* [OpenELEC para Raspberry Pi 2](http://releases.openelec.tv/OpenELEC-RPi2.arm-5.0.6.img.gz?mirrorlist)
* [Licencia MPEG-2](http://www.raspberrypi.com/mpeg-2-license-key/): Necesaria para reproducir la señal TDT.

## Instalación

A continuación se indica el proceso de montaje paso a paso. Vamos a dividirlo en cuatro bloques.

### Instalación OpenELEC

Las instrucciones que siguen se corresponden con una instalación desde un equipo con Linux. En caso de utilizar Windows o MacOSX habrá que buscar las alternativas. Por ejemplo en las [instrucciones oficiales de instalación de OpenELEC](http://wiki.openelec.tv/index.php/HOW-TO:Installing_OpenELEC/Creating_The_Install_Key#tab=DiskImage) sí que se dan instrucciones específicas para cada sistema. La web oficial de Raspberry Pi también tiene una [guía bastante buena](http://www.raspberrypi.org/documentation/installation/installing-images/README.md).

1. Abrimos un terminal.
2. Bajamos la imagen de OpenELEC para Raspberry Pi 2:

        $ wget http://releases.openelec.tv/OpenELEC-RPi2.arm-5.0.6.img.gz

3. Insertamos la tarjeta microSD en el lector de tarjetas del ordenador.
4. Averiguamos la ruta del dispositivo de la tarjeta:

        $ df -h
        S.ficheros             Tamaño Usados  Disp Uso% Montado en
        /dev/sda3                 61G    44G   14G  76% /
        none                     4,0K      0  4,0K   0% /sys/fs/cgroup
        udev                     1,9G    12K  1,9G   1% /dev
        tmpfs                    390M   1,3M  389M   1% /run
        none                     5,0M      0  5,0M   0% /run/lock
        none                     2,0G    27M  1,9G   2% /run/shm
        none                     100M    84K  100M   1% /run/user
        /dev/mmcblk0p2           3,4G   1,6M  3,4G   1% /media/edumoreno/3f46971c-8bb7-4f8a-9095-2862537e6191
        /dev/mmcblk0p1           256M   104M  153M  41% /media/edumoreno/1765-7DD1

5. La mejor forma de averiguar los dispositivos correctos es ejecutar `df -h` antes y después de insertar la tarjeta. En mi caso aparecen dos particiones sobre el dispositivo `/dev/mmcblk0` (p1 y p2 son el sufijo de las particiones; en algunos lectores de tarjetas nos podría aparecer `/dev/sdb1` y `/dev/sdb2` por ejemplo, lo que indicaría que el dispositivo es `/dev/sdb`).

6. Desmontamos las particiones montadas de la tarjeta:

        $ sudo umount /dev/mmcblk0p1
        $ sudo umount /dev/mmcblk0p2

7.  Copiamos a la tarjeta la imagen de OpenELEC bajada en el paso 2:

        $ gunzip OpenELEC-RPi2.arm-5.0.6.img.gz -c | sudo dd of=/dev/mmcblk0 bs=2M
        $ sudo sync

### Conexión de piezas

Cuando termine el último punto de la sección anterior (tardará más o menos dependiendo de la velocidad de la tarjeta), sacaremos la tarjeta microSD del lector y la insertaremos en la ranura de la Raspberry. Conectamos el cable HDMI entre el televisor y la Raspberry. Conectamos el adaptador TDT y el adaptador Wifi al concentrador USB. Alimentamos el concentrador y enlazamos la entrada del concentrador con una de las entradas USB de la Raspberry. Finalmente alimentamos la Raspberry con un cable USB - microUSB desde el concentrador hacia la Raspberry. El primer arranque de OpenELEC sirve para redimensionar las particiones de la tarjeta microSD para aprovechar toda su capacidad. Al terminar el proceso se reiniciará automáticamente y esta vez sí, terminará apareciendo el interfaz de Kodi. A partir de ahora trabajaremos con Kodi para configurar una serie de cosas.

### Configuración Kodi

El primer arranque muestra un asistente en el que entre otras cosas se selecciona el idioma de los menús, la conexión a internet y si queremos activar los servicios SSH y Samba. Necesitamos activar el primero para poder averiguar más adelante el número de serie de la Raspberry para contratar la licencia MPEG-2.

Una vez terminado el asistente acudimos a la siguiente ruta de los menús para activar el adaptador Wifi:

    Sistema / OpenELEC / Red / Redes inalámbricas / Activo

Una vez activo conectamos a nuestro punto de acceso siguiendo esta secuencia de menús:

    Sistema / OpenELEC / Conexiones / engancho mi AP

#### Instalación de TVheadend

Lo siguientes pasos nos permiten activar el sistema de gestión del TDT:  

    Sistema / Ajustes / Add-ons / Comprobar actualizaciones
    Sistema / Ajustes / Add-ons / Conseguir Add-ons / OpenELEC Mediacenter OS Add-ons / Repositorio de Add-ons / Unofficial OpenELEC (RPi2/arm) Add-ons / Instalar
    Sistema / Ajustes / Add-ons / Comprobar actualizaciones
    Sistema / Ajustes / Add-ons / Conseguir Add-ons / Todos los Add-ons / Servicios / tvheadend / Instalar
    Sistema / Ajustes / Add-ons / Add-ons desactivados / Tvheadend HTSP Client / Activar
    Sistema / Ajustes / TV en directo / General / Activado

#### Configuración de Tvheadend

Tvheadend tiene arquitectura cliente/servidor. Lo que manipulamos a través de Kodi es la parte cliente. La parte servidora se sirve por TCP/IP a través de los puertos 9981 y 9982. El primer puerto ofrece un interfaz web al que podemos pues entrar con un navegador accediendo a la dirección http://ip-de-raspberry:9981

La IP de la raspberry la podremos averiguar acudiendo a la ruta:

    Sistema / OpenELEC / Conexiones

Por cierto que ya que estamos en esta ruta, se recomienda editar la conexión y poner una IP fija en el apartado IPv4, ya que como veremos, el interfaz web de Tvheadend es muy potente.

Una vez dentro de la consola web de Tvheadend seguimos los siguientes pasos para activar el decodificador de TDT y añadir los canales:  

    Configuration / General / Language settings / Available / Spanish; Castilian -> Selected / Save configuration
    Configuration / DVB Inputs / TV Adapters / Realtek RTL2832 / Parameters / Basic Settings / Enabled / Save
    Configuration / DVB Inputs / Networks / Add / Type: DVB-T Network / Network Name: TDT / Create
    Configuration / DVB Inputs / Muxes / Add (ver lista más adelante)
    Configuration / DVB Inputs / TV Adapters / Realtek RTL2832 / Parameters / Basic Settings / Networks / (seleccionamos TDT) / Save
    Configuration / DVB Inputs / Services / Map All / Check availability / Map

La lista de Muxes depende de la provincia en la que nos encontremos. [Aquí](http://www.tdt1.com/) por ejemplo podemos encontrar las frecuencias. Los muxes que utilizo en Zaragoza son los siguientes:

![TDT Muxes](/images/posts/muxes.png)

Todos ellos se han introducido con los siguientes parámetros:

* Bandwidth: 8MHz
* Constellation: QAM/64
* Transmission Mode: 8k
* Resto de parámetros: AUTO

### Instalación licencia MPEG-2

Aunque por la arquitectura cliente/servidor de Tvheadend podremos visualizar la señal TDT desde otros dispositivos que tengamos en la misma red (como por ejemplo con nuestro teléfono Android con [esta aplicación](https://play.google.com/store/apps/details?id=org.tvheadend.tvhguide) instalada), si queremos ver la televisión en el propio Kodi, vamos a necesitar adquirir la licencia para utilizar el hardware de decodificación MPEG-2 que hay incluido en el procesador Broadcom 2836 de la Raspberry Pi 2. La licencia tiene un coste de £2.40 Para ello necesitamos primero averiguar el número de serie de la Raspberry siguiendo estos pasos:

1. Conectamos por SSH con la Raspberry (password = `openelec`):

        $ ssh root@ip-de-raspberry

2. Obtenemos el número de serie:

        OpenELEC:~ # cat /proc/cpuinfo | fgrep Serial
        Serial		: 0000000029bcaeeb

3. Adquirimos la licencia acudiendo a la [Raspberry Pi Store](http://www.raspberrypi.com/mpeg-2-license-key/).
4. Aproximadamente un día después recibiremos por correo un código que ahora tendremos que instalar en la Raspberry.
5. Apagamos Kodi/OpenELEC desde menú.
6. Cuando se termine de apagar la Raspberry, quitamos la alimentación y sacamos la tarjeta microSD.
7. Insertamos la tarjeta en el lector del ordenador. Se montarán las dos nuevas particiones que contiene la distribución OpenELEC. La partición más pequeña es la de arranque donde está el kernel Linux y una serie de ficheros de configuración de Raspberry Pi que actúan a modo de BIOS. Entre esos ficheros vamos a modificar el `config.txt`. Casi al final hay una serie de claves que comienzan por `decode_`. La primera de ellas es `decode_MPG2`. Descomentaremos la línea quitando la almohadilla que hay al principio y sustituiremos el valor por el que hemos obtenido por correo al adquirir la licencia. Guardamos el fichero, extraemos la tarjeta microSD y la volvemos a insertar en la Raspberry.

FIN