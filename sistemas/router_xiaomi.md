---
layout: default
permalink: /sistemas/router_xiaomi.html
---

# Router Xiaomi MiWiFi 3G

## Enlaces

* [Serie de artículos de Carlos Monge sobre OpenWRT instalado en Xiaomi MiWiFi 3G](https://elblogdelazaro.gitlab.io//tags/#openwrt)
* [Página del router en OpenWRT](https://openwrt.org/toh/xiaomi/mir3g): Incluye instrucciones para debrick.
* [Xiaomi WiFi Router 3G](https://forum.openwrt.org/t/xiaomi-wifi-router-3g/5377): Hilo del foro OpenWRT sobre el Xiaomi MiWiFi 3G router.
* [Xiaomi Wifi Router 3G - 18.06.X / feedback and help](https://forum.openwrt.org/t/xiaomi-wifi-router-3g-18-06-x-feedback-and-help/19840): Hilo del foro OpenWRT sobre el firmware 18.06 en el Xiaomi MiWiFi 3G router.

## Actualización firmware

Siguiendo [este artículo](https://elblogdelazaro.gitlab.io/articles/openwrt-actualizar-firmware/):

1. Bajar el paquete pinchando uno de los enlaces siguientes según si se desea la versión de desarrollo o la estable de la [página de soporte del router en OpenWRT](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_miwifi_3g):
    * Estable: Firmware OpenWrt Upgrade URL
    * Desarrollo: Firmware OpenWrt snapshot Upgrade URL
2. En el interfaz web (Luci) acudir a la ruta `System > Backup / Flash Firmware`.
3. En la sección `Flash new firmware image` pulsar el botón `Examinar...` y seleccionar el fichero .tar bajado en el punto anterior.
4. Pulsar el botón `Flash image...`.
5. En la siguiente página confirmar el flasheo comprobando si se quiere los checksums.
6. Cuando termine el proceso habremos perdido los paquetes adicionales. Instalarlos conectando por SSH y ejecutando los siguientes comandos:

        # opkg update
        # opkg install luci
        # opkg install luci-ssl
        # /etc/init.d/uhttpd start
        # /etc/init.d/uhttpd enable
7. Si se desea la interfaz en español (no se aconseja), instalar también:

        # opkg install luci-i18n-base-es

## Configuración desde cero

1. Instalar Luci:

        # opkg update
        # opkg install luci
        # opkg install luci-ssl
        # /etc/init.d/uhttpd start
        # /etc/init.d/uhttpd enable

2. Descarga de paquetes por HTTPS:

    1. Instalar:

            # opkg update
            # opkg install ca-certificates

    2. Editar el fichero `/etc/opkg/distfeeds.conf` y cambiar http por https.

3. Crear usuario normal y permitirle usar sudo:

    1. Ejecutar:

            # opkg update
            # opkg install shadow-useradd
            # useradd miusuario
            # passwd miusuario
            # mkdir /home
            # mkdir /home/miusuario
            # chown miusuario:miusuario /home/miusuario
            # opkg install sudo

    2. Editar el fichero `/etc/passwd` y poner shell al usuario nuevo:

            miusuario:x:1000:1000::/home/miusuario:/bin/ash

    3. Ejecutar el comando `visudo` y añadir la siguiente línea bajo la correspondiente a root:

            miusuario ALL=(ALL) ALL
