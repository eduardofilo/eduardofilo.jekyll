---
layout: default
permalink: /sistemas/emulacion.html
---

# Emulación

## Enlaces

* [Emuladores en OpenELEC](http://misapuntesde.com/post.php?id=502)
* [Configuración PiGRRL-2](http://apuntes.eduardofilo.es/2016/07/21/PIGRRL-2.html)
* [Managing ROMs](https://github.com/retropie/retropie-setup/wiki/Managing-ROMs)
* [MAME FAQ](http://wiki.mamedev.org/index.php/FAQ:Games): Resuelve dudas sobre peculiaridades de algunos juegos. Por ejemplo sobre el arranque de [Joust](http://wiki.mamedev.org/index.php/FAQ:Games#Joust).

## Empaquetado de ROMs MAME

Primero hay que localizar los ficheros que componen la ROM. Hay varios tipos (explicados [aquí](https://github.com/retropie/retropie-setup/wiki/Managing-ROMs#step-5--rebuild-a-rom-set)). Una forma de ir a lo seguro es localizar sus piezas gracias a los hash SHA1 que se pueden encontrar en los ficheros [.DAT](https://github.com/retropie/retropie-setup/wiki/Managing-ROMs#quick-reference) y luego hacer un paquete ZIP sin compresión.

Para generar un archivo ZIP con compresión nula en Linux, se consigue por ejemplo con el siguiente comando lanzado desde el directorio donde se encuentren los ficheros que queremos empaquetar:

```bash
zip -0 rom.zip *
```

El nombre del archivo (en el ejemplo `rom.zip`) es importante para que el emulador reconozca la ROM. También lo obtendremos del fichero `.DAT`.
