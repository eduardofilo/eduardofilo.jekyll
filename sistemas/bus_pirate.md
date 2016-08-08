---
layout: default
permalink: /sistemas/bus_pirate.html
---

# Bus Pirate

## Enlaces

* [Bus Pirate - Documentación oficial](http://dangerousprototypes.com/docs/Bus_Pirate/es)

## Conexión

```bash
$ screen /dev/buspirate 115200 8N1
```

## Adaptador USB-UART

Bus Pirate se puede utilizar como un adaptador USB-UART configurándolo en modo UART y activar el macro de modo transparente. Para ello seguir la siguiente secuencia:

```
HiZ>m3
Set serial port speed: (bps)
 1. 300
 2. 1200
 3. 2400
 4. 4800
 5. 9600
 6. 19200
 7. 38400
 8. 57600
 9. 115200
10. BRG raw value

(1)>5
Data bits and parity:
 1. 8, NONE *default
 2. 8, EVEN
 3. 8, ODD
 4. 9, NONE
(1)>1
Stop bits:
 1. 1 *default
 2. 2
(1)>1
Receive polarity:
 1. Idle 1 *default
 2. Idle 0
(1)>1
Select output type:
 1. Open drain (H=Hi-Z, L=GND)
 2. Normal (H=3.3V, L=GND)

(1)>2
Ready
UART>(0)
 0.Macro menu
 1.Transparent bridge
 2. Live monitor
 3.Bridge with flow control
UART>(1)
UART bridge
Reset to exit
Are you sure? y
```
