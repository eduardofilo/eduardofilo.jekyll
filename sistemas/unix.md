---
layout: default
permalink: /sistemas/unix.html
---

# UNIX

## Cheat sheets

*  [Colección de Carlos Fenollosa](http://mmb.pcb.ub.es/~carlesfe/#unix)
*  [Tricks de Carlos Fenollosa](http://cfenollosa.com/misc/tricks.txt)
*  [Bash Cheat Sheet](http://www.johnstowers.co.nz/blog/pages/bash-cheat-sheet.html)
*  [Programar en Bash, pequeño manual de referencia](http://www.linuxhispano.net/2010/06/08/bash-manual-referencia-cheat-sheet-mini/)

## Comandos útiles

*  `strace -e file [command]`: runs `command`, printing out any time a file is opened or checked.
*  `strace -e file,network,process [command]`: the same as above, but also printing network process and subcommands run.
*  `strace -e file,process -f [command]`: the -f parameter follows forks -- in case it's not main command but a subshell that you're interested in.
*  `strace -p [PID]`: Connect to pid PID and start tracing.
*  `route -n`: Tabla de rutas del sistema.
*  `netstat -nr`: Tabla de rutas del sistema.
*  `du -h --max-depth=1 .`: Tamaño de un directorio y sus subdirectorios directos.
*  `find [directorio] ! -user [usuario] -ls`: Lista los ficheros que NO pertenecen a un usuario.
*  `badblocks -swv /dev/sda`: Bloquear sectores defectuosos (sustituir `/dev/sda` por el dispositivo que corresponda.
*  `dpkg --configure -a`: Soluciona problemas con paquetes mal instalados.
*  `mkdosfs -F 32 -v -n "" /dev/sdc1`: Formato de partición en FAT32.
*  `du -sh */ | sort -h`: Muestra los directorios del directorio actual ordenados por tamaño (en formato humano) indicando su tamaño.
*  `cat fichero.txt | awk '{print $5}'`: Imprime la quinta columna (separando por espacios) de cada linea del fichero.
*  `cat fichero.txt | cut -d' ' -f5`: Imprime la quinta columna (separando por espacios) de cada linea del fichero.
*  `cat fichero.txt | sed -e 's/ /\n/g'`: Sustituye todos los espacios del fichero por retornos de carro.
*  `netstat -ntu|grep :80|wc -l`: número de conexiones al servidor HTTP.
*  `netstat -ntu|grep :21|wc -l`: número de conexiones al servidor FTP.
*  `crontab -e`: Añadir un job a cron.
*  `sudo badblocks /dev/sda > badblocks.txt; sudo fsck -l badblocks.txt /dev/sda`: Bloqueo de sectores defectuosos del disco duro ([fuente](http://tech.chandrahasa.com/2013/06/09/how-to-check-your-hard-disk-for-bad-blocks-in-ubuntu/)).
*  `sudo blkid`: Lista los dispositivos de bloques (discos) disponibles en el sistema.
*  `sudo nmap -PR -sP 192.168.1.0/24`: Descubrir todos los equipos presentes en la red `192.168.1.0`.

## Búqueda de ficheros que contienen una cadena

{% highlight bash %}
#!/bin/bash
SAVEIFS=$IFS
IFS=$(echo -en "\n\b")
for file in `find .`
do
fgrep "[cadena a buscar]" $file > /dev/null 2>&1
if [ $? -eq 0 ]; then
echo $file
fi
done
IFS=$SAVEIFS
{% endhighlight %}

En realidad el script anterior hace lo mismo que el simple comando siguiente:

{% highlight bash %}
fgrep -rl "[cadena a buscar]" .
{% endhighlight %}

## Ajustes de permisos a ficheros y directorios por separado

{% highlight bash %}
# Para los ficheros:
find . ! -type d -exec chmod 664 {} \;
# Para los directorios:
find . -type d -exec chmod 775 {} \;
{% endhighlight %}

## Renombrado de ficheros de mayúsculas a minúsculas

([Fuente](http://aptgetanarchy.org/node/75))

{% highlight bash %}
#!/bin/sh
for f in *; do
g=`expr "xxx$f" : 'xxx\(.*\)' | tr '[A-Z]' '[a-z]'`
mv "$f" "$g"
done
{% endhighlight %}

## Redirección de salidas

Para redirigir ambas salidas de un programa (estandar y error) hacer lo siguiente:
{% highlight bash %}
COMANDO > FICHERO_O_DISPOSITIVO 2>&1
{% endhighlight %}

En [esta página](http://sc.tamu.edu/help/general/unix/redirection.html) se documenta con más detalle este tema.

## Ejecución remota de aplicaciones XWindow

 1.  Abrir el servidor X (Cygwin)
 2.  Iniciar sesión remota: ssh -X [usuario]@[máquina]
 3.  Ejecutar la aplicación

## MySQL

*  Acceso: mysql -u root -p
*  Listar bases de datos: show databases;
*  Abrir una base de datos: use [NombreBBDD];
*  Listar tablas: show tables


## Ficheros de configuración importantes

*  `/etc/security/limits.conf`: Configuration file for the pam_limits module. Permite limitar el número de ficheros abiertos por el sistema, el número de procesos, etc.

## Solución al problema de los alias (alternatives) de Java6 en Ubuntu

Los paquetes de Java 6 (1.6) en Ubuntu tienen problemas a la hora de ajustar los alias en /etc/alternatives cuando antes ha estado instalada otra versión (1.5 por ejemplo). Se puede forzar la generación de los alias mediante las siguientes ordenes:
{% highlight bash %}
update-java-alternatives --list
sudo update-java-alternatives --set [elegir el identificador de la lista que muestra el comando anterior]
{% endhighlight %}

## Bits SUID, SGID y sticky

[Manual de LuCAS](http://lucas.olea.org/Manuales-LuCAS/doc-unixsec/unixsec-html/node56.html)

## Autentificación automática por SSH

Conseguiremos que la autentificación del cliente se haga por medio de una pareja de claves privada/pública en lugar de con identificador de usuario/password. Primero generamos la pareja de claves pública-privada ejecutando en el cliente `ssh-keygen`:
{% highlight bash %}
$ ssh-keygen  -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/user/.ssh/id_rsa.
Your public key has been saved in /home/user/.ssh/id_rsa.pub.
The key fingerprint is:
xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx user@machine
{% endhighlight %}

Las claves se almacenan por defecto en `~/.ssh/`, quedando el directorio así:
{% highlight bash %}
$ ls -l
total 12
-rw-------  1 user user  883 2005-08-13 14:16 id_rsa
-rw-r--r--  1 user user  223 2005-08-13 14:16 id_rsa.pub
-rw-r--r--  1 user user 1344 2005-08-04 02:14 known_hosts
{% endhighlight %}

Los ficheros `id_rsa` e `id_rsa.pub` contienen respectivamente las claves privada y pública. El fichero `known_hosts` contiene la lista de las claves públicas de las máquinas reconocidas.

Ahora se debe copiar la clave pública al servidor, al fichero `~/.ssh/authorized_keys`. Para ello se utiliza el comando ssh-copy-id:
{% highlight bash %}
$ ssh-copy-id -i ~/.ssh/id_rsa.pub user@machine1
$ ssh-copy-id -i ~/.ssh/id_rsa.pub user@machine2
{% endhighlight %}

`ssh-copy-id` es un script que se conecta a la máquina y copia el archivo (indicado por la opción `-i`) en `~/.ssh/authorized_keys`, y ajusta los permisos a los valores adecuados.

Si no se dispone del programa `ssh-copy-id` se puede realizar una copia manual a la máquina remota del fichero conteniendo la clave pública (por ejemplo usando `scp` o `sftp`) y añadir su contenido al fichero `~/.ssh/authorized_keys`.

Ahora la conexión debería funcionar sin necesidad de introducir la clave. Si no es así es posible que sea un problema de permisos en los ficheros. Los permisos correctos deben ser similares a estos:
{% highlight bash %}
$ chmod go-w ~ ~/.ssh
$ chmod 600 ~/.ssh/authorized_keys
{% endhighlight %}

La conexión SSH se realizará indicando el fichero con la clave privada como argumento de la siguiente forma:
{% highlight bash %}
ssh -i ~/.ssh/id_rsa user@machine
{% endhighlight %}

(Si el nombre del fichero con la clave privada es precisamente el del ejemplo, es decir `id_rsa`, creo que no es necesario indicarlo con la opción `-i`).


## Configuración de Firefox para ejecución de applets Java

([Fuente](http://www.java.com/es/download/help/5000010500.xml#14))

* Vaya al subdirectorio de complementos, situado dentro del directorio de instalación de Mozilla.
{% highlight bash %}
	cd `<directorio de instalación de Mozilla>`/plugins  # Normalmente /usr/lib/firefox/plugins
{% endhighlight %}
o
{% highlight bash %}
	cd `<home del usuario>`/.mozilla/plugins
{% endhighlight %}

* En el directorio actual, cree un vínculo simbólico al archivo del JRE ns7/libjavaplugin_oji.so. Escriba:\\
{% highlight bash %}
	ln -s `<directorio de instalación del JRE>`/plugin/i386/ns7/libjavaplugin_oji.so
{% endhighlight %}
* Inicie el navegador Mozilla o reinícielo si ya se estaba ejecutando. Tenga en cuenta que, si se está ejecutando algún otro componente de Mozilla (como Messenger, Composer, etc.) deberá también reiniciarlo.
* Vaya a Editar > Preferencias. En la categoría Avanzadas, seleccione Activar Java.

## Organización de menús cuando se mezclan aplicaciones KDE y Gnome

GNU/Linux nos permite tener varios sistemas de escritorio diferentes instalados y funcionando, pero inevitablemente nos encontramos con una mezcla de opciones y programas de cada entorno en los menús principales. Existen aplicaciones precisamente para limpiar automáticamente las entradas del menú que no corresponden a tu sistema de escritorio habitual, y dejarlas apartadas y ordenadas de alguna manera. Con Gnome y KDE instalados a la vez, hay dos programas para aquellos Gnomeros que han querido probar KDE y para los KDEeros que han querido probar Gnome.

*  [Gnome Menu Extended](http://www.gtk-apps.org/content/show.php/Gnome+Menu+Extended+%28Debian+Package%29?content=73515) es el propio menú normal de Gnome, pero incluye una carpeta donde se guardan todas las aplicaciones y opciones de KDE. Se instala fácilmente descargando el paquete para cualquier distribución: Debian (y Ubuntu), Slackware o directamente el código fuente para compilarlo. Una vez instalado, se activa yendo a Preferencias -> Add KDE Menu. Y si quieres recuperar el menú como estaba, también tiene la opción de restaurarlo.
*  [K Menu Gnome](http://www.kde-apps.org/content/show.php/K+Menu+Gnome+%28Debian+Package%29?content=31031&amp;PHPSESSID=39c71268b399effce8c57dbf8ff09e16) es un menú exactamente igual que el KMenu original, pero incluye una carpeta donde residen todas las aplicaciones de Gnome, en sistemas que tienen ambos escritorios instalados. Está disponible para Debian (y Ubuntu), Slackware, Fedora y el código fuente para compilarlo en cualquier sistema.

## Error "error while loading shared libraries: ..."

Runtime error. The linker hasn't found your libraries. Either they are not installed properly or the linker doesn't know where they are (most probably in `/usr/local/lib`). To get your linker to update its list of libraries type:
{% highlight bash %}
ldconfig /usr/local/lib
{% endhighlight %}
or as a temporary measure:
{% highlight bash %}
export LD_LIBRARY_PATH="/usr/local/lib"
{% endhighlight %}

## Compartir ficheros con Samba

Aparte de instalar y configurar Samba (fichero `/etc/samba/smb.conf`) hay que dar de alta los usuarios UNIX que se usarán a través de Samba y asignarles un password para el acceso por el mismo. Esto se hace con el comando:
{% highlight bash %}
sudo smbpasswd -a usuario
{% endhighlight %}

## Migración masiva de usuarios

([Fuente](http://www.esemanal.com.mx/articulos.php?id_sec=5&id_art=4583))

Para los casos en los que sea necesario replicar los usuarios de un servidor Linux a otro o en los que se vaya a migrar a un servidor con más recursos, el siguiente procedimiento puede ser de utilidad.

Los escenarios son varios, desde los servidores que ejecutan algún tipo de base de datos, los que tienen ciertas aplicaciones, los que alojan páginas Web, etcétera. Para fines de la demostración pensaremos que el servidor está dedicado como servidor de archivos, mismos que se almacenan en el home de cada uno de los usuarios.
NOTA: El presente procedimiento da por hecho que se hayan realizado las configuraciones necesarias en el nuevo servidor.

Primero, lo que debe respaldarse es la lista de usuarios con su respectiva contraseña.
El archivo `/etc/passwd` contiene las cuentas de los usuarios en el sistema bajo el siguiente formato de ejemplo:

{% highlight text %}
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/
nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
nitsuga:x:500:500::/home/nitsuga:/bin/bash
nitsuga2:x:501:501::/home/nitsuga2:/bin/bash
nitsuga3:x:502:502::/home/nitsuga3:/bin/bash
{% endhighlight %}

Como se observa, el segundo campo respectivo al hash de la contraseña no se muestra. La contraseña se encuentra en el archivo `/etc/shadow`
{% highlight text %}
root:$1$/7zmwgAa$Jd5ja7nsC4nTm
O3s0.Z1j1:13445:0:99999:7:::
bin:*:13445:0:99999:7:::
daemon:*:13445:0:99999:7:::
adm:*:13445:0:99999:7:::
nitsuga:$1$QwPqN0Vc$dn9OIyE3HQUh5W4Yh/.aQ.:13498:2:1:1:::
nitsuga2:$1$635CQht0$rFIbilzKqfc1zStqeOwlk/:13496:2:45:7:::
nitsuga3:$1$635CQht0$rFIbilzKqfc1zStqeOwlk/:13496:2:45:7:::
{% endhighlight %}


Se procederá a unir el usuario con su contraseña utilizando el comando “pwunconv” para “desactivar” el shadow, quedando así las contraseñas en el archivo passwd.
{% highlight text %}
root:$1$/7zmwgAa$Jd5ja7nsC4n
TmO3s0.Z1j1:0:0:root:/root:/bin/bash
bin:*:1:1:bin:/bin:/sbin/nologin
daemon:*:2:2:daemon:/sbin:/sbin/
nologin
adm:*:3:4:adm:/var/adm:/sbin/nologin
nitsuga:$1$QwPqN0Vc$dn9OIyE3HQUh5W4Yh/.aQ.:500:500::/home/
nitsuga:/bin/bash
nitsuga2:$1$635CQht0$rFIbilzKqfc1zStqeOwlk/:501:501::/home/nitsuga2:/bin/bash
nitsuga3:$1$635CQht0$rFIbilzKqfc1zStqeOwlk/:502:502::/home/nitsuga3:/bin/bash
{% endhighlight %}

### Depuración de /etc/passwd

Se copiará el archivo `/etc/passwd` a uno de trabajo `/etc/passwd.migracion`. Ahora se editará el archivo y se quitarán todos los usuarios propios del sistema (root, usuarios de demonios, etcétera) dejando sólo los usuarios que van a ser autenticados.
{% highlight text %}
nitsuga:$1$QwPqN0Vc$dn9OIyE3HQUh5W4Yh/.aQ.:500:500::/home/nitsuga:/bin/bash
nitsuga2:$1$635CQht0$rFIbilzKqfc1zStqeOwlk/:501:501::/home/nitsuga2:/bin/bash
nitsuga3:$1$635CQht0$rFIbilzKqfc1zStqeOwlk/:502:502::/home/nitsuga2:/bin/bash
{% endhighlight %}

También se copiará el archivo `/etc/group` a `/etc/group.migracion`
{% highlight text %}
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
nitsuga:x:500:
nitsuga2:x:501:
nitsuga3:x:502:
nitsuga8:x:507:
{% endhighlight %}

Y se editará para dejar sólo los grupos de los usuarios:
{% highlight text %}
nitsuga:x:500:
nitsuga2:x:501:
nitsuga3:x:502:
{% endhighlight %}

Ahora se respaldará el home de los usuarios, suponiendo que se encuentra bajo el directorio/home, se hará lo siguiente desde raíz (/):
{% highlight text %}
[root@localhost /]# tar -cpzvf home.tgz home/
{% endhighlight %}

En el que las banderas:

*  c = crea el archivo
*  p = preserva los permisos
*  z = comprime el archivo .tar generado
*  v = da salida detallada
*  f = especifica el archivo a crear (para este caso home.tgz)

Ahora bien, se realizará la transferencia de los archivos home.tgz, passwd.migracion y group.migracion al nuevo servidor:
{% highlight text %}
[root@localhost /]# scp /home.tgz root@nuevoservidor

[root@localhost /]# scp /etc/passwd.migracion root@nuevoservidor

[root@localhost /]# scp /etc/group.migracion root@nuevoservidor
{% endhighlight %}

Una vez en el nuevo servidor se deberá verificar que no se repitan tanto los UID como los GID entre los dos servidores.
Se realizará:
{% highlight text %}
[root@localhost /]# cp –p home.tgz / ; tar –zxvf home.tgz

[root@localhost /]# cp –p passwd.migracion /etc ; pwunconv ; cat passwd.migracion >> passwd; pwconv

[root@localhost /]# cp –p group.migracion /etc ; cat group.migracion >> group
{% endhighlight %}

## Eliminar petición password en sudo

Es necesario reconfigurar el fichero `/etc/sudoers` para que no se solicite el password del usuario a la hora de hacer sudo, dado que necesitamos que se haga sudo desde un proceso que no tendrá interacción con el usuario. Para conseguir esto hay que hacer dos cosas:

1.  Incorporar el usuario que nos interesa al grupo `sudo` del sistema
2.  Situar al final del fichero de configuración `/etc/sudoers` lo siguiente:

{% highlight text %}
%sudo ALL=NOPASSWD: ALL
{% endhighlight %}

Hay que fijarse que la linea anterior normalmente ya aparece en el fichero pero comentada con una almohadilla. Se puede aprovechar la linea quitando el carácter almohadilla del principio, pero hay que tener en cuenta que no es suficiente con eso. Hay que mover la linea al final del fichero ya que las lineas siguientes pueden sobreescribir su efecto.

**Importante**: La edición del fichero `/etc/sudoers` sólo se puede hacer con el comando `visudo`. Este comando hay que lanzarlo con `sudo` a su vez, por lo que se hará de la siguiente forma:
{% highlight bash %}
sudo visudo
{% endhighlight %}

## Proxy HTTP en consola

Setting up proxy at Firefox do not have effects at console, which means your wget, ssh, apt-get, yum etc do not access through the proxy you set at Firfox browser. To setup http proxy at console, you can do as bellow, assume the proxy IP is 219.93.2.113 and port 3128:
{% highlight bash %}
export http_proxy='http://219.93.2.113:3128/'
{% endhighlight %}

Remember, you have to specified http://, and to know more about export, check out HERE.
To clear your http proxy and use back yours, do this:
{% highlight bash %}
export http_proxy=''
{% endhighlight %}

## Convertir nombres de ficheros de ISO a UTF-8

Al migrar una web, o al copiar un sistema de archivos, te puedes encontrar con nombres de ficheros en otras codificaciones de caracteres. Mediante el siguiente comando transformaríamos los nombres de ficheros desde ISO-8869-1 a UTF-8:
{% highlight bash %}
convmv -r -f ISO-8859-1 -t UTF-8  --notest *
{% endhighlight %}

## Backup de un FileSystem

Backup:
{% highlight bash %}
dd if=/dev/hdx | gzip > /path/to/image.gz
{% endhighlight %}

Restauración:
{% highlight bash %}
gzip -dc /path/to/image.gz | dd of=/dev/hdx
{% endhighlight %}

## Manipulación de PDFs

División en múltiples ficheros (uno por página):
{% highlight bash %}
pdftk largepdfile.pdf burst
{% endhighlight %}

Fusión de varios ficheros en uno:
{% highlight bash %}
pdftk *.pdf cat output onelargepdfile.pdf
{% endhighlight %}

## Obtener hash MD5 de una cadena
{% highlight bash %}
echo -n "<cadena>"|md5sum
{% endhighlight %}

## System + MySQL backup script
{% highlight bash %}
#!/bin/bash
# System + MySQL backup script
# Full backup day - Sun (rest of the day do incremental backup)
# Copyright (c) 2005-2006 nixCraft `<http://www.cyberciti.biz/fb/>`
# This script is licensed under GNU GPL version 2.0 or above
# Automatically generated by http://bash.cyberciti.biz/backup/wizard-ftp-script.php
# ---------------------------------------------------------------------

### System Setup ###
DIRS="/var/spool/sms /var/log/smstools /root"
BACKUP=/tmp/backup.$$
NOW=$(date +"%d-%m-%Y")
INCFILE="/var/tar-inc-backup.dat"
DAY=$(date +"%a")
# echo $DAY >> /root/dates
FULLBACKUP="Sun"

### MySQL Setup ###
MUSER="mysqluser"
MPASS="mysqlpwd"
MHOST="localhost"
MYSQL="$(which mysql)"
MYSQLDUMP="$(which mysqldump)"
GZIP="$(which gzip)"

### FTP server Setup ###
FTPD="//incremental"
FTPU="ftpuser"
FTPP="ftppwd"
FTPS="ftphost"
NCFTP="$(which ncftpput)"

### Other stuff ###
EMAILID="user@domain.com"

### Start Backup for file system ###
[ ! -d $BACKUP ] && mkdir -p $BACKUP || :

### See if we want to make a full backup ###
if [ "$DAY" == "$FULLBACKUP" ]; then
  FTPD="//full"
  FILE="fs-full-$NOW.tar.gz"
  tar -zcvf $BACKUP/$FILE $DIRS
else
  i=$(date +"%Hh%Mm%Ss")
  FILE="fs-i-$NOW-$i.tar.gz"
  tar -g $INCFILE -zcvf $BACKUP/$FILE $DIRS
fi

### Start MySQL Backup ###
# Get all databases name
DBS="$($MYSQL -u $MUSER -h $MHOST -p$MPASS -Bse 'show databases')"
for db in $DBS
do
 FILE=$BACKUP/mysql-$db.$NOW-$(date +"%T").gz
 $MYSQLDUMP -u $MUSER -h $MHOST -p$MPASS $db | $GZIP -9 > $FILE
done

### Dump backup using FTP ###
#Start FTP backup using ncftp
ncftp -u"$FTPU" -p"$FTPP" $FTPS<<EOF
mkdir $FTPD
mkdir $FTPD/$NOW
cd $FTPD/$NOW
lcd $BACKUP
mput *
quit
EOF

### Find out if ftp backup failed or not ###
if [ "$?" == "0" ]; then
 rm -f $BACKUP/*
else
 T=/tmp/backup.fail
 echo "Date: $(date)">$T
 echo "Hostname: $(hostname)" >>$T
 echo "Backup failed" >>$T
 mail  -s "BACKUP FAILED" "$EMAILID" <$T
 rm -f $T
fi
{% endhighlight %}