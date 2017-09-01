---
layout: default
permalink: /desarrollo/vagrant.html
---

# Vagrant

## Instalación

Instalar VirtualBox de la distribución (`virtualbox` en Ubuntu) y bajar el instalable de Vagrant de su [sitio web](https://www.vagrantup.com/downloads.html).

## Creación de entorno

Desde el directorio raíz de nuestro proyecto de desarrollo, ejecutar:

```
$ vagrant init
```

Esto crea el fichero `Vagrantfile` que mantendrá la configuración de nuestro entorno. Este fichero conviene incluirlo en el control de versiones.

Modificamos el fichero `Vagrantfile` para que use la máquina que nos interesa. En el ejemplo vamos a usar `ubuntu/xenial64` (consultar [aquí](https://app.vagrantup.com/boxes/search) el catálogo completo de máquinas).

```
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
end
```

Cuando se levante por primera el entorno configurado en el `Vagrantfile` se bajará la máquina. Si queremos adelantar este proceso podemoa bajar la máquina con el siguiente comando:

```
$ vagrant box add ubuntu/xenial64
```

Ahora ya podemos levantar el entorno y conectar con él:

```
$ vagrant up
$ vagrant ssh
```

Tal y como se indica en el log del arranque de la máquina (durante el `vagrant up`), el directorio del proyecto de la máquina host se monta sobre `/vagrant` de la máquina guest:

```
==> default: Mounting shared folders...
    default: /vagrant => /home/edumoreno/git/niubit_lms
```

## Provisión de componentes

La máquina que hemos instalado (`ubuntu/xenial64`) viene con Python3 preinstalado. Vamos a instalar Django de forma controlada con Vagrant para que pueda reproducir esa instalación de forma automática si creamos este entorno en otro lugar. Para ello escribimos un script que luego integramos en el `Vagrantfile` de la siguiente forma:

```
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provision "shell", inline: <<-SHELL
    #!/usr/bin/env bash
    apt-get update
    apt-get install -y python3-pip
    pip3 install Django
  SHELL
end
```

Si no habíamos arrancado la máquina todavía, el script se ejecutará en el primer arranque. Si ya lo habíamos hecho habrá que decirle a Vagrant que ejecute la configuración de provisioning:

```
$ vagrant reload --provision
```
