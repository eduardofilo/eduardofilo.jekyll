---
layout: post
title: "Micro placas"
date: 2014-12-20 12:52:00
categories: placas raspberry_pi
published: true
---

Llevo un tiempo pendiente del relativamente nuevo mundo de las micro placas popularizadas gracias a Arduino y Raspberry Pi. De entre las dos anteriores me quedo con la segunda al ser más una persona de soft que de hard y tener Raspberry Pi más potencial en este sentido. Además siendo que la diferencia de precio es pequeña, por qué resistirse a tener un Linux completo corriendo en la placa. Está claro que esto tiene repercusiones en cuanto a estabilidad, seguridad y sobre todo autonomía energética, pero como digo, en mi caso es más habitual que esto pese menos que las ventajas que me aporta construir sobre Linux.

A continuación una lista con algunas de las placas de este tipo que me llaman la atención:

* [Raspberry Pi](http://www.raspberrypi.org/)
* [Banana Pi](http://www.bananapi.org/)
* [Hummingboard](http://www.solid-run.com/products/hummingboard/)
* [BeagleBoard](http://beagleboard.org/)
* [pdDuino](http://www.pcduino.com/)
* [Cubieboard](http://cubieboard.org/)
* [UDOO](http://www.udoo.org/)
* [ODROID](http://www.hardkernel.com/main/main.php)

Hasta ahora los únicos proyectos que he puesto en marcha han sido de computación, es decir, sin componente hardware. Han servido para delegar un par de funciones que antes ejecutaba directamente sobre mi PC principal. Concretamente:

* Gestor de descargas.
* Servidor git para proyectos personales privados que no quiera tener en [GitHub](https://github.com/eduardofilo).

Raspi consume 3.5W como máximo, así que con ella se puede uno permitir que estos servicios funcionen las 24 horas del día. Ya no sólo por la ventaja de cara a la factura eléctrica, sino también por evitar "quemar" un caro PC en tareas de proceso puntual pero que requieren alta disponibilidad (se ve muy claro en el caso del servidor git).

Pero a partir de mayo de 2015 tengo el plan de que este tipo de placas se conviertan en mis procesadores principales de propósito general, es decir que sustituyan a mi actual portátil. Y es que he financiado el proyecto [Pi-Top](http://pi-top.com/) por el cual recibiré las piezas en esa fecha para montar mi propio portátil a medida. Y para construirlos/mejorarlos desde entonces, ya que el kit incluye los planos/archivos para poder imprimir la carcasa en una impresora 3D. La última versión de Pi-Top está anunciado que soporte de serie al menos UDOO, BeagleBone, ODROID y Banana Pi, aparte por supuesto de Raspberry Pi.