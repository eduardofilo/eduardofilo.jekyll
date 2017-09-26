---
layout: default
permalink: /desarrollo/python.html
---

# Python

## Enlaces

### Aprendizaje

* [The Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/intro/learning/)
* [Alter model to add “through” relationship to order a ManytoMany field](https://stackoverflow.com/questions/26348260/alter-model-to-add-through-relationship-to-order-a-manytomany-field-django-1)
* [How to Reset Migrations](https://simpleisbetterthancomplex.com/tutorial/2016/07/26/how-to-reset-migrations.html)

### Módulos interesantes

* [django-tinymce](https://github.com/aljosa/django-tinymce)
* [django-autocomplete-light](https://github.com/yourlabs/django-autocomplete-light)

## Entorno Django

Para tener un entorno aislado (sin depender con los paquetes y versiones del sistema), instalar primero `pip` de Python3. Se puede hacer instalando el paquete `python3-pip` de Ubuntu, pero dado que interesa actualizar a la última versión, es mejor instalarlo de forma independiente bajando el script `get-pip.py` de [aquí](https://pip.pypa.io/en/stable/installing/) ejecutándolo así:

```
$ sudo python3 get-pip.py
```

Después ejecutar en terminal:

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
(djangodev) $ django-admin startproject project01
```

## Creación de aplicación Django

Desde el directorio del proyecto (donde se encuentre el fichero `manage.py`) ejecutamos:

```
(djangodev) $ python manage.py startapp app01
```

Para incorporar los modelos de la nueva aplicación al mantenimiento automático que proporciona el módulo `admin` de Django, hay que incorporar al fichero `project01/settings.py` lo siguiente en la sección `INSTALLED_APPS`:

```
INSTALLED_APPS = [
    'app01.apps.App01Config',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Luego ejecutamos el siguiente comando para generar las migraciones a partir de los modelos definidos en la app:

```
(djangodev) $ python manage.py makemigrations app01
```

Finalmente ejecutamos las migraciones propiamente dichas:

```
(djangodev) $ python manage.py migrate
```

Para poder utilizar el módulo `admin` de Django, hay que crear al menos un usuario:

```
(djangodev) $ python manage.py createsuperuser
```
