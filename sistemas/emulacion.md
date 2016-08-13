---
layout: default
permalink: /sistemas/emulacion.html
---

# Emulación

## Enlaces

* [Emuladores en OpenELEC](http://misapuntesde.com/post.php?id=502)
* [Configuración PiGRRL-2](http://apuntes.eduardofilo.es/2016/07/21/PIGRRL-2.html)

## Empaquetado de ROMs MAME

El archivo ZIP en que suelen empaquetarse las ROMs debe tener compresión nula. En Linux se consigue por ejemplo con el siguiente comando lanzado desde el directorio donde se encuentren los ficheros que queremos empaquetar:

```bash
zip -0 rom.zip *
```

El nombre del archivo (en el ejemplo `rom.zip`) es importante para que el emulador reconozca la ROM.
