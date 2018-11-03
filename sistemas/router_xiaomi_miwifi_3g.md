---
layout: default
permalink: /sistemas/router_xiaomi.html
---

# Router Xiaomi MiWiFi 3G

## Enlaces

* [Serie de artículos de Carlos Monge sobre OpenWRT instalado en Xiaomi MiWiFi 3G](https://elblogdelazaro.gitlab.io//tags/#openwrt)
* [Hilo del foro OpenWRT sobre el Xiaomi MiWiFi 3G router](https://forum.openwrt.org/t/xiaomi-wifi-router-3g/5377)

## Actualización firmware

Siguiendo [este artículo](https://elblogdelazaro.gitlab.io/articles/openwrt-actualizar-firmware/):

1. Bajar el paquete pinchando el enlace tras el rótulo `Firmware OpenWrt snapshot Upgrade URL` en la [página de soporte del router en OpenWRT](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_miwifi_3g).
2. En el interfaz web (Luci) acudir a la ruta `System > Backup / Flash Firmware`.
3. En la sección `Flash new firmware image` pulsar el botón `Examinar...` y seleccionar el fichero .tar bajado en el punto anterior.
4. Pulsar el botón `Flash image...`.
5. En la siguiente página confirmar el flasheo comprobando si se quiere los checksums.
6. Cuando termine el proceso habremos perdido el paquete Luci. Instalarlo conectando por SSH y ejecutando los siguientes comandos:
        # opkg update
        # opkg install luci
        # opkg install luci-ssl
        # /etc/init.d/uhttpd start
        # /etc/init.d/uhttpd enable
7. Si se desea la interfaz en español (no se aconseja), instalar también:
        # opkg install luci-i18n-base-es
