---
layout: post
title: "Octoprint en Anet A8"
date: 2018-06-13 22:40:00
published: false
---

![Octoprint](/images/posts/octoprint.jpg)

Instalación de Raspberry Pi sobre impresora 3D Anet A8 para ejecutar Octoprint.

## Imágen de sistema

Aunque es posible [instalar manualmente Octoprint](https://discourse.octoprint.org/t/setting-up-octoprint-on-a-raspberry-pi-running-raspbian/2337) sobre una instalación Raspbian estándar, existe una [imágen para grabar directamente sobre la tarjeta microSD llamada OctoPi](https://octoprint.org/download/). Dado que la Raspberry Pi y por tanto su sistema se va dedicar exclusivamente para esta función, se prefiere esta alternativa.

## Modelo de Raspberry Pi elegido

A pesar de que la utilización de una Raspberry Pi Zero no está recomendada por problemas de rendimiento que pueden terminar afectando a las impresiones, en mi experiencia no he sufrido ningún percance y la forma y bajo consumo de la Raspberry Pi Zero, lo que permite alimentarla desde la misma fuente de la impresora, resulta perfecta para esta instalación.

Sospecho que los posibles problemas están vinculados al uso de la webcam. Eligiendo la cámara adecuada (que soporte MJPG de forma nativa) y no abusando del vídeo en streaming creo que se deja un margen de seguridad adecuado para poder aprovechar las ventajas de la versión Zero W de la Raspberry Pi.

## Conexión serie entre Anet A8 y Raspberry Pi

Octoprint se comunica con la impresora por medio de una conexión serie. Esta conexión puede fácilmente establecerse a través de USB. De hecho el puerto serie del microcontrolador Atmel que gobierna la impresora está puenteado a un adaptador serie/USB que hay sobre la placa (CH340G). Utilizar esta conexión USB resulta muy aparatoso por el tipo de conectores que implica, así que se ha preferido liberar el puerto serie del microcontrolador para poder utilizarlo directamente.

Estudiando el [esquemático de la placa](/images/posts/octoprint_ANET3D_Board_Schematic.png) se ve que las siguientes secciones son las implicadas en este asunto (se han marcado en azul las zonas de más interés):

![Puerto serie](/images/posts/octoprint_puerto_serie.png)

Podemos ver cómo el puerto serie del microcontrolador (pines AOFI y AIFO) está puenteado al chip CH340G (U6) por medio de un par de resistencias de 0Ω que actúan como puente. Tendremos que retirar de la placa dichas resistencias R52 y R53.

Una vez hecho, soldaremos unos pines en la ubicación J8 de la placa (al menos la mía venía con los agujeros en la PCB sin los pines soldados). En esta [foto de alta resolución de la placa](/images/posts/octoprint_hires_pcb.jpg) podemos ver bien tanto la ubicación de los puentes J8 como las resistencias que hay que retirar:

![Sección de la PCB](/images/posts/octoprint_hires_pcb_subsection.jpg)

Sólo queda poner un par de jumpers entre los pines siguientes de J8:

* 3-5
* 4-6

Con esto conseguimos que el puerto serie del microcontrolador aparezca disponible en el conector J3. Si antes utilizábamos el puerto USB de la PCB para algún cometido, hay que entender que al realizar esta modificación deja de estar disponible, pero tenemos la opción de reactivarlo cambiando los jumpers a la siguiente disposición:

* 1-3
* 2-4

Como la orientación de la PCB en la impresora es distinta a la del esquemático, se muestra ahora con claridad el resultado final, es decir cómo deben disponerse los dos jumpers para que el puerto serie aparezca en el conector J3 y el hueco dejado por las resistencias R52 y R53:

![Puentes](/images/posts/octoprint_puentes.jpg)

Como vemos los puentes deben apuntar hacia el rótulo BLE. Seguramente se designa así porque la sustitución habitual del puerto USB sería un adaptador Bluetooth que podría adaptarse al conector J3.

Sólo queda localizar en el conector J3 los pines del puerto serie del microcontrolador recien redirijidos y los de alimentación (5V y GND). En este punto podríamos conectar la Raspberry Pi con simples cables de pin, pero dada la cercanía en el GPIO de la Raspberry Pi del puerto serie y de los terminales de alimentación, me decidí a preparar una pequeña placa adaptadora para el conector J3 de la PCB de la impresora.

El conector J3 de la impresora tiene el siguiente pineado según el esquemático:

![Conector J3](/images/posts/octoprint_j3.png)

## Desactivación de BT y activación de puerto serie
https://www.abelectronics.co.uk/kb/article/1035/raspberry-pi-3-and-zero-w-serial-port-usage

Por medio de `raspi-config` desactivar el terminal asociado al puerto serie físico y habilitar el puerto (pregunta las dos cosas dentro de la misma opción `Interfacing options > Serial`).

## Configuración cámara

* [How can I change mjpg-streamer parameters on OctoPi?](https://discourse.octoprint.org/t/how-can-i-change-mjpg-streamer-parameters-on-octopi/203)
* [Webcams known to work](https://github.com/foosel/OctoPrint/wiki/Webcams-known-to-work)
* [Available mjpg-streamer configuration options](https://discourse.octoprint.org/t/available-mjpg-streamer-configuration-options/1106)

## Instalación plugin M84 Motors Off

https://plugins.octoprint.org/plugins/m84motoff/

    cd ~/OctoPrint
    ./venv/bin/pip install "https://github.com/ntoff/Octoprint-M84MotOff/archive/master.zip"

## G-code
http://marlinfw.org/meta/gcode/

## Apps
https://play.google.com/store/apps/details?id=com.kabacon.octoremote
https://play.google.com/store/apps/details?id=fr.yochi76.printoid.phones.trial

## Plugins intalados:
M84 Motors Off
TouchUI
DisplayLayerProgress
