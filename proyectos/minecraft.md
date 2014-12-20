---
layout: default
permalink: /proyectos/minecraft.html
---

# Minecraft

## Enlaces

### Varios

*  [How to Create A Minecraft Server Like Mine on your Raspberry Pi](http://picraftbukkit.webs.com/pi-minecraft-server-how-to)
*  [Video de educador que usa Minecraft](https///www.youtube.com/watch?v=-mTf3j2koJA)
*  [Minecraft Edu](http://minecraftedu.com/)
*  [Minecraft Edu Wiki](http://services.minecraftedu.com/wiki/Main_Page)
*  [Tutorials/Setting up a server](http://minecraft.gamepedia.com/Setting_up_a_server)
*  [Server Commands](http://minecraft.gamepedia.com/Server_commands)
*  [Minecraft Server Manager](http://msmhq.com/)
*  [How to Run Low-Cost Minecraft on a Raspberry Pi for Block Building on the Cheap](http://www.howtogeek.com/173044/how-to-run-low-cost-minecraft-on-a-raspberry-pi-for-block-building-on-the-cheap/) (!)
*  [MineCraftPi - A Raspberry Pi MineCraft Server Image!](http://everyday-tech.com/minecraftpi-a-raspberry-pi-minecraft-server-image/): Minecraft se arranca automáticamente desde `/etc/rc.local`.

### Mecanismos

* [Tutoriales/Mecanismos](http://minecraft-es.gamepedia.com/Tutoriales/Mecanismos)
* [Introduction to Redstone](http://www.minecraft101.net/redstone/redstone-basics.html)

### Servidores

*  [MCServer](http://mc-server.org/)
*  [Mineserver](http://mineserver.be/)
*  [Descarga servidor oficial](https///minecraft.net/download)
*  [Mirror de Bukkit y Spigot para sortear DMCA](https///savebukkit.org/)

### Configuraciones

*  [server.properties](http://minecraft.gamepedia.com/Server.properties)
*  [Bukkit.yml fichero de configuración de Craftbukkit y Spigot](http://wiki.bukkit.org/Bukkit.yml/es)
*  [spigot.yml fichero de configuración de Spigot](http://www.spigotmc.org/wiki/spigot-configuration-spigot-yml/)

### Plugins recomendables

*  [NoSpawnChunks](http://dev.bukkit.org/bukkit-plugins/nospawnchunks/): Prevents spawn chunks being loaded into memory for all worlds on the server.
*  [WorldBorder](http://dev.bukkit.org/bukkit-plugins/worldborder/)
*  [ClearLagg](http://dev.bukkit.org/bukkit-plugins/clearlagg/)
*  [NoLagg](http://dev.bukkit.org/bukkit-plugins/nolagg/)
*  [pTweaks](http://dev.bukkit.org/bukkit-plugins/ptweaks-remove-all-server-lag/): pTweaks is a server optimization tool. This plugin will redefine how your server loads, stores and manages chunks.
*  [Dynmap](http://dev.bukkit.org/bukkit-plugins/dynmap/): Mapa 2D dinámico.
*  [WorldEdit](http://dev.bukkit.org/bukkit-plugins/worldedit/): Editor de mundos. Comandos [aquí](http://wiki.sk89q.com/wiki/WorldEdit/Reference). Documentación [aquí](http://wiki.sk89q.com/wiki/WorldEdit).

## Ejecución Servidor en Raspberry Pi

### Comandos para arrancarlo

```bash
#Servidor oficial
sudo java -Xms256M -Xmx496M -jar /home/mine/minecraft_server/minecraft_server.1.8.jar nogui

#Spigot
sudo java -Xms256M -Xmx496M -jar /home/mine/spigot/spigot.jar nogui
```

### Settings aconsejadas

([Fuente](http://www.raspberrypi.org/forums/viewtopic.php?t=27889))

*server.properties*

```
#Minecraft server properties
#Thu Jan 03 16:16:28 WET 2013

white-list=false #Si se activa sólo se permitirá la incorporación a la partida de determinados jugadores
level-seed=
view-distance=4
server-ip=
allow-nether=false
gamemode=1 #Creative
enable-query=false #Si se permite obtener información del servidor mediante el protocolo GameSpy4
hardcore=false
level-type=DEFAULT
enable-rcon=false
motd=Raspberry Pi Minecraft server
spawn-monsters=false #No se generan monstruos
spawn-protection=16
difficulty=0 #Peaceful
allow-flight=true #En modo Creative creo que se permite siempre
generator-settings=
spawn-npcs=false #No se generan vecinos (villagers)
level-name=world #Determina la carpeta donde se almacena el mundo. Por tanto sirve para cambiar de mundo
generate-structures=true #Determina si se generan estructuras (como ciudades)
online-mode=false
max-players=6 #Máximo de jugadores admitidos
server-port=25565
max-build-height=208 #Altura máxima permitida para construir, aunque el terreno generado puede superarla
pvp=false #No se permiten daños entre jugadores
spawn-animals=true #Se generan animales
snooper-enabled=false #Si se envían periódicamente datos a snoop.minecraft.net
op-permission-level=4 #Nivel máximo de permisos de op
announce-player-achievements=true #Se anuncian los logros obtenidos por los jugadores
debug=false
force-gamemode=true #Fuerza la configuración del servidor a cada jugador
```

*bukkit.yml*

```
settings:
  allow-end: false #Desactiva el End (http://minecraft.gamepedia.com/The_End)
```

*spigot.yml*

```
world-settings:
  default:
    view-distance: 4
```

*plugins/WorldBorder/config.yml*

```
cfg-version: 11
message: Has alcanzado el límite de este mundo.
round-border: false
debug-mode: false
whoosh-effect: true
portal-redirection: true
knock-back-dist: 3.0
timer-delay-ticks: 5
remount-delay-ticks: 0
dynmap-border-enabled: true
dynmap-border-message: Has alcanzado el límite de este mundo.
player-killed-bad-spawn: false
deny-enderpearl: true
fill-autosave-frequency: 30
bypass-list-uuids: []
fill-memory-tolerance: 500
worlds:
  taller1:  # Nombre del mundo a limitar
    x: 0
    z: 0
    radiusX: 80
    radiusZ: 80
    wrapping: false
```

### Comandos útiles

#### Servidor

* `gamerule doDaylightCycle false`: Paramos el reloj.
* `time set 6000`: Pone el reloj al mediodía # Fijamos el reloj al mediodía.
* `tp <jugador> <x> <y> <z>`: Teleporta a un jugador a una posición.
* `setworldspawn 0 20 0`: Definimos el punto de spawn del mundo.
* `toggledownfall`: Activa/desactiva la lluvia.
* `gamerule doFireTick false`: Evita que se propague el fuego.
* `gamerule doMobSpawning false`: Evita que se generen Mobs (pasivos y enemigos). Util en modo creativo para evitar distracciones.

#### Plugins

##### WorldBorder

* `wb shape square`: Ajustamos el tipo de borde a cuadrado.
* `wb <nombre_mundo> set 100 spawn`: Ajustamos el radio del borde del mundo.
* `wb <nombre_mundo> fill`: Forzamos la generación del mundo dentro del límite.
* `wb <nombre_mundo> trim`: Eliminamos el mapeado del mundo que queda fuera del límite.
* `wb setmsg "Has alcanzado el límite de este mundo."`: Ajustamos el mensaje que ven los jugadores al alcanzar el límite.

##### Dynmap

* `dynmap fullrender <world-name>`: Genera el mapa que inicialmente aparece en negro.

##### WorldEdit

* `//wand`: Te otorga la herramienta para definir regiones cúbicas o planas.
* `//walls <material>`: Rellena la región definida con `wand` con el material indicado.

### Montaje de un mundo plano para talleres

Antes de empezar paramos el servidor. Generamos un mundo nuevo cambiando lo siguiente en `server.properties`:

```
level-type=FLAT
level-name=taller1
allow-nether=false
gamemode=1 #Creative
difficulty=0 #Peaceful
generate-structures=false #No se generan estructuras (como ciudades)
spawn-npcs=false #No se generan vecinos (villagers)
online-mode=false
spawn-animals=false #No se generan animales
force-gamemode=true #Fuerza la configuración del servidor a cada jugador
```

Arrancamos el servidor. Por medio de comandos lo modelamos:

```
setworldspawn 0 20 0
wb shape square
wb taller1 set 80 spawn # Lo limitamos a un cuadrado de 160x160 en torno al punto de spawn
wb taller1 fill # Generamos el mundo
wb fill confirm
wb taller1 trim # Eliminamos lo que sobra
wb trim confirm
wb setmsg "Has alcanzado el límite de este mundo." # Ajustamos mensajes
gamerule doDaylightCycle false # Paramos el reloj
time set 6000 # Pone el reloj al mediodía # Fijamos el reloj al mediodía
toggledownfall # Desactivamos la lluvia
```