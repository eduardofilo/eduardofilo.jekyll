---
layout: default
permalink: /sistemas/kodi.html
---

# Kodi/OpenELEC

## Desactivar un canal de PelisALaCarta
Si durante las búsquedas, alguno de los canales bloquea el progreso, seguramente habrá habido algún cambio en el código del sitio que el plugin no es capaz de interpretar. Habrá que esperar a que salga una nueva versión del plugin, pero mientras tanto se puede desactivar ese canal acudiendo a la ruta siguiente:

    /storage/.kodi/addons/plugin.video.pelisalacarta/channels

Allí localizamos el archivo .xml correspondiente al canal, lo editamos y ponemos a `false` la propiedad `active`.
