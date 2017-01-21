---
layout: post
title: "Micro placas"
date: 2014-12-20 12:52:00
published: true
---

![Raspberry Pi Logo](/images/posts/Raspi_Colour_R.png)

Llevo un tiempo pendiente del relativamente nuevo mundo de las micro placas, popularizadas gracias a Arduino y Raspberry Pi. De entre las dos anteriores me quedo con la segunda al ser una persona más de soft que de hard y tener Raspberry Pi más potencial en este sentido. Además siendo que la diferencia de precio es pequeña, por qué resistirse a tener un Linux completo corriendo en la placa. Está claro que esto tiene repercusiones en cuanto a estabilidad, seguridad y sobre todo autonomía energética, pero como digo, en mi caso es más habitual que esto pese menos que las ventajas que me aporta construir sobre Linux.

A continuación una lista con algunas de las placas de este tipo que se pueden encontrar:

* [Raspberry Pi](http://www.raspberrypi.org/)
* [Banana Pi](http://www.bananapi.org/p/product.html) y [Banana Pro](http://www.lemaker.org/)
* [Hummingboard](http://www.solid-run.com/products/hummingboard/)
* [BeagleBoard](http://beagleboard.org/)
* [pdDuino](http://www.pcduino.com/)
* [Cubieboard](http://cubieboard.org/)
* [UDOO](http://www.udoo.org/)
* [ODROID](http://www.hardkernel.com/main/main.php)
* [Up](http://up-shop.org/)
* [Orange Pi](http://www.orangepi.org/orangepipc/)
* [Asus Tinker Board](http://cpc.farnell.com/asus/90mb0qy1-m0eay0/tinker-board-2gb-1-8ghz-4k-gb/dp/SC14363)

Hasta ahora los únicos proyectos que he puesto en marcha han sido de computación, es decir, sin componente hardware, que es otro de los usos importantes que se les suelen dar. Han servido para delegar un par de funciones que antes ejecutaba directamente sobre mi PC principal. Concretamente:

* Gestor de descargas.
* Servidor git para proyectos personales privados que no quiera publicar en [GitHub](https://github.com/eduardofilo).

Raspi consume 3.5W como máximo, así que con ella se puede uno permitir que estos servicios funcionen las 24 horas del día. Ya no sólo por las ventajas que tiene de cara a la factura eléctrica, sino también por evitar "quemar" un caro PC en tareas de proceso puntual pero que requieren alta disponibilidad (se ve muy claro en el caso del servidor [git](http://git-scm.com/)).

También vienen muy bien estas placas para adosarlas a los televisores modernos y montar cosas como media centers (por ejemplo con [XBMC-Kodi](http://kodi.tv/)) y consolas de videojuegos retro por emulación (con distribuciones como [Lakka](http://www.lakka.tv/)), sin ruidos de ventiladores, ocupando muy poco espacio y consumiendo poca energía.

A partir de mayo de 2015 tengo el plan de utilizar este tipo de placas como procesadores principales de propósito general, es decir sustituyendo a mi actual portátil. Y es que he financiado el proyecto [Pi-Top](http://pi-top.com/) por el cual recibiré las piezas en esa fecha para montar mi propio portátil. Y para construir/mejorar todos los que quiera desde entonces, ya que el kit incluye los planos/archivos para poder imprimir la carcasa en una impresora 3D, y el resto de componentes son tan accesibles/asequibles como las propias micro placas. La última versión de Pi-Top está anunciado que soporte de serie al menos UDOO, BeagleBone, ODROID y Banana Pi, aparte por supuesto de Raspberry Pi.

La placa que más me gusta en la actualidad (y que seguramente mueva las entrañas del Pi-Top inicial) es la [ODROID-C1](http://www.hardkernel.com/main/products/prdt_info.php?g_code=G141578608433). 4 cores ARMv7 a 1.5GHz, Mali450, 1GB de RAM DDR3, Gigabit Ethernet, zócalo eMMC y 4 puertos USB [por 37€](http://www.raspipc.es/public/home/index.php?ver=tienda&accion=verArticulo&idProducto=1187).
