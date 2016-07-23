---
layout: default
permalink: /sistemas/ubuntu_phone.html
---

# Ubuntu Phone

## Activar SSH:

        sudo service ssh start
        sudo setprop persist.service.ssh true
        sudo reboot

## Permitir cambios en /

        sudo mount -o remount,rw /

## Ejecutar en modo desktop

        gsettings set com.canonical.Unity8 usage-mode Windowed

## Retornar a interfaz teléfono

        gsettings set com.canonical.Unity8 usage-mode Staged
