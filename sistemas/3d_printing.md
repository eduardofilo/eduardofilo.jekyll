---
layout: default
permalink: /sistemas/3d_printing.html
---

# 3D Printing
<iframe width="854" height="480" src="https://www.youtube.com/embed/LMOrumVvI-s" frameborder="0" allowfullscreen></iframe>

## Enlaces

* [Lista de vídeos en canal Dron3D 8A sobre "Anet A8"](https://www.youtube.com/watch?v=TRGdz0yRO7c&list=PLr9CknKcEHUlm3PTex04n78AiWuMqgWlv)
* [Lista de vídeos en canal Dron3D 8A sobre "Impresión 3D - Conceptos y ayuda"](https://www.youtube.com/watch?v=YhcDe49rHW8&list=PLr9CknKcEHUnk8RUK-SkszBbB5VvvIz_-)
* [Lista de vídeos en canal Dron3D 8A sobre "Impresión 3D - Software"](https://www.youtube.com/watch?v=ZdFok0dGJVA&list=PLr9CknKcEHUk1pihCmI-h94qjx_0DQTkD)
* [Lista de vídeos en canal Dron3D 8A sobre "Impresión 3D - Tipos de Material"](https://www.youtube.com/watch?v=4xHwCWh7yGQ&list=PLr9CknKcEHUlTFZdiqnLILHZzD8tTEEUd)
* [Anet A8 3DPrint.wiki](https://3dprint.wiki/reprap/anet/a8)
* [Trello de "Comunidad 3D [ES]"](https://trello.com/b/X1HL9kIf/03anet-a8)
* [Firmware alternativo](https://linuxgnublog.org/es/lidiando-con-mi-impresora-3d-anet-a8-firmware/)
* Instalación de 2 MosFET: [Post](http://moderntoil.com/?p=850) y [STLs](https://www.thingiverse.com/thing:2086107)
* [Como calibrar el control de temperatura PID de la impresora 3D](https://3dinvasion.com/blog/como-calibrar-el-control-de-temperatura-pid-de-la-impresora-3d/)

## Hardware / Componentes / Repuestos

* [Rodamiento lineal](https://m.banggood.com/es/LM8UU-8mm-Linear-Ball-Bearing-Bush-Steel-for-CNC-Router-Mill-Machine-p-906777.html)
* [Rodamiento lineal sin bolas](https://www.amazon.es/dp/B06X6LD76G)
* [Rodamiento lineal largo](https://m.banggood.com/es/LM8LUU-8mm-Long-Type-Linear-Motion-Ball-Bearing-Slide-Bushing-CNC-Part-p-994394.html?rmmds=detail-middle-buytogether-auto)
* [Enchufe de corriente de entrada](https://www.amazon.es/dp/B00FFY3Q0C)
* [Alargador lector microSD](https://www.amazon.es/dp/B06XX5GZTG)
* [Conectores rápidos JST](https://www.amazon.es/dp/B06XX5MY4J)
* [Módulo MOSFET](https://www.amazon.es/dp/B071XQZ576)
* [Módulo MOSFET](https://www.amazon.es/dp/B071XHN284)
* [Sensor de posición inductivo](https://www.amazon.es/dp/B01G6P102E)
* Cinta de carrocero especial impresoras: [Amazon](https://www.amazon.es/dp/B071X4216X), [Banggood](https://www.banggood.com/es/50mmx50m-50mm-Wide-3D-Printer-Blue-Tape-Reprap-Bed-Tape-Masking-Tape-For-3D-Printer-Parts-p-1103934.html)

## Mejoras Anet A8

* [Mejoras sobre montaje original](https://www.youtube.com/watch?v=gLBd4UJASeE)
* [Soporte para las herramientas](https://www.thingiverse.com/thing:1539675)
* [Conectores en ventiladores](https://www.youtube.com/watch?v=53idlnO-D-0)
* [Alargador lector microSD](https://www.youtube.com/watch?v=UjbZNyR9wSI)
* [MOSFET exterior](https://www.youtube.com/watch?v=r77z5vjibOI)
* [Soldar conector cama caliente](https://www.youtube.com/watch?v=rIALeyU7qAA)
* Refuerzos eje X: [v1](https://www.youtube.com/watch?v=r9TOwpRwL_I) y [v2](https://www.thingiverse.com/thing:2189694)
* [Interruptor y ventilador de fuente](https://www.youtube.com/watch?v=BCvEKxvmbHo)
* [Ventilador de placa base](https://www.youtube.com/watch?v=1sY4XBeMPWU)

## Parámetros impresión Anet A8

### General

* X (Width): 220mm
* Y (Depth): 220mm
* Z (Height): 240mm
* Build plate shape: Rectangular
* Heated bed: Checked
* Bed center is 0,0,0: Unchecked
* Material diameter: 1.75mm
* Nozzle size: 0.4mm

### Cura 3.1

* `Quality > Layer Height`: 0.2 mm [0.1-0.3] Altura de Capa.
* `Quality > Initial Layer Height`: 0.2 mm [0.1-0.3] Altura de la capa inicial. Una capa inicial más final mejora la adherencia a la cama.
* `Quality > Initial Layer Line Width`: 100 %. Permite aumentar ligeramente la anchura de las líneas de la primera capa para aumentar la adherencia a la cama. Básicamente inyecta un poco más de material.
* `Shell > Wall Thickness`: 1.2 mm [0.8-2.0] Grosor de la piel. Debe ser múltiplo de `Layer Height`.
* `Shell Top/Bottom Thickness`: 1.2 mm [0.8-2.0] Grosor de la piel superior e inferior. Cuando la densidad de relleno es menor que 20%, se puede producir caída de la capa superior. En ese caso se recomienda un mínimo de 1.2mm.
* `Infill > Infill Density`: 20 % [0-100] Tanto por ciento de relleno en el interior. Dependerá de la resistencia deseada para la pieza. Si no va a recibir cargas se puede utilizar 10 o incluso 0%.
* `Material > Printing Temperature`: 220 ºC [170 - 230] en PLA; [230-250] en ABS. Temperatura de extrusión del material.
* `Material > Build Plate Temperature`: 50ºC [40-60] en PLA; [60-90] en ABS. Temperatura de la cama caliente.
* `Material > Diameter`: 1.75 mm. Diámetro de la entrada del extrusor.
* `Material > Flow`: 100 %. Sirve para aportar más o menos material si observamos que en las impresiones aparecen bultos o huecos entre las líneas o capas.
* `Material > Enable Retraction`: Marcado. Retrae el hilo cuando el cabezal se tiene que desplazar sin imprimir.
* `Material > Retraction Distance`: 4.5mm. Cantidad de material recogido durante la retracción.
* `Material > Retraction Speed`: 40 mm/s. Velocidad de la retracción.
* `Material > Retraction Minimum Travel`: 1.5 mm. Distancia mínima de desplazamiento del extrusor a partir de la que se aplica retracción.
* `Speed > Print Speed`: 30 mm/s [10-120] Velocidad de impresión. A menor velocidad más precisión de impresión. No se recomienda pasar de 40-60.
* `Speed > Infill Speed`: 40 [10-120] Velocidad de impresión del relleno.
* `Speed > Outer Wall Speed`: 20 [10-120] Velocidad de impresión de las caras externas.
* `Speed > Inner Wall Speed`: 30 [10-120] Velocidad de impresión de las caras internas. Suele ser un valor intermedio entre `Infill Speed` y `Outer Wall Speed`.
* `Travel > Combing Mode`: Realiza los desplazamientos sobre superficies ya impresas para evitar retracción o que gotee el extrusor.
    * `Off`: Desplazamientos en línea recta.
    * `All`: Desplaza siempre por zonas impresas.
    * `No Skin`: Desplaza por el interior de las piezas, evitando la superficie.
* `Travel > Z Hop When Retracted`: Marcado. Levanta un poco el extrusor cuando se inicia un desplazamiento para evitar colisiones con las partes ya impresas.
* `Cooling > Enable Print Cooling`: Activa el ventilador de la boquilla del extrusor.
    * Marcado: En PLA.
    * Desmarcado: En ABS.
* `Cooling > Regular Fan Speed`: 30 %. La velocidad del ventilador antes de alcanzar el tiempo mínimo de impresión de la capa, momento en que se acelera hasta alcanzar la velocidad máxima.
* `Cooling > Maximum Fan Speed`: 70 %. Velocidad máxima del ventilador cuando se alcanza el tiempo mínimo de impresión de la capa.
* `Cooling > Initial Fan Speed`: 0 %. Velocidad del ventilador al comienzo de la impresión.
* `Cooling > Regular Fan Speed at Height`: 0.5 mm. Altura de capa a partir de la cual el ventilador empezará a girar a la velocidad `Regular`. Este retraso en el encendido del ventilador sirve para mejorar la adhesión de la pieza a la cama.
* `Cooling > Minimum Layer Time`: 10 seg. Tiempo mínimo de impresión de una capa. Si no se alcanza antes de empezar una nueva la impresora esperará.
* `Cooling > Lift Head`: Desmarcado. Aparta la cabeza cuando no se alcanza el tiempo mínimo de impresión de la capa para evitar que el extrusor gotee sobre la misma. Es mejor bajar la velocidad de impresión en este tipo de piezas pequeñas en las que no se alcance el tiempo mínimo de impresión de capa.
* `Support > Generate Support`: Marcado. Generar soporte para partes en voladizo.
* `Support > Support Placement`: Everywhere
    * `Touching Builplate`: Sólo hace soportes en las partes en voladizo sobre la cama.
    * `Everywhere`: Hace soportes en todas las partes que lo necesiten.
* `Build Plate Adhesion`: Skirt
    * `Skirt`: Hace una línea alrededor de la piza en la primera capa. Básicamente sirve para cebar el extrusor.
    * `Brim`: Hace más amplia la primera capa para aumetar la adhesión a la cama.
    * `Raft`: Hace una malla alrededor y debajo de la pieza para aumentar la adhesión a la cama. Puede ser difícil de despegar.
* `Special Modes`: All at Once. Usar siempre esta opción.
