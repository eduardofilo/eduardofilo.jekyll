---
layout: default
permalink: /desarrollo/python.html
---

# Python

## Enlaces

*  [The Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/intro/learning/)

## Entorno Django

Para tener un entorno aislado (sin depender con los paquetes y versiones del sistema), instalar primero `pip` de Python3 (paquete `python3-pip` de Ubuntu). Después ejecutar en terminal:

```
$ sudo pip3 install virtualenv
$ virtualenv --python=`which python3` djangodev
$ source djangodev/bin/activate
(djangodev) $ pip install Django
```

Cada vez que se quiera adaptar el entorno de la sesión del terminal a este entorno aislado, hay que ejecutar el penúltimo comando anterior (`source`).

## Creación de proyecto Django

Desde el directorio donde queremos que se cree ejecutamos:

```
(djangodev) $ django-admin startproject project_dir
```

## Creación de aplicación Django

Desde el directorio del proyecto (donde se encuentre el fichero `manage.py`) ejecutamos:

```
(djangodev) $ python manage.py startapp app_dir
```
