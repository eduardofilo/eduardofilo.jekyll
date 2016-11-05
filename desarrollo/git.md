---
layout: default
permalink: /desarrollo/git.html
---

# Git

## Enlaces

* [Libro Pro Git en español](http://git-scm.com/book/es)
* [Cheat Sheat](http://cheat.errtheblog.com/s/git)
* [git - la guía sencilla](http://rogerdudler.github.com/git-guide/index.es.html) :exclamation:
* [Git Tutorials & Training by Atlassian](http://atlassian.com/git) :exclamation:
* [Detached HEAD en Git](http://mundogeek.net/archivos/2015/08/11/detached-head-en-git/)
* [Github git tutorial](https://try.github.io/levels/1/challenges/1)
* [La Parábola de Git @ CAPSiDE HQ](https://www.youtube.com/watch?v=sXudMl5x_5g)

## Comandos básicos

Config:

```bash
$ git config --global user.name "Eduardo Moreno"
$ git config --global user.email user@dominio.com
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global core.editor "subl -w"
```

Alternativamente se pueden hacer todos los cambios simultáneamente editando el fichero `~/.gitconfig`. Una configuración podría ser:

```
[user]
        name = Eduardo Moreno
        email = user@dominio.com
[alias]
        co = checkout
        ci = commit
        st = status
[core]
        editor = subl -w
```

Creación repositorio (local; crea el subdirectorio `.git`):

```bash
$ cd first_app
$ git init
```

Add:

```bash
$ git add .
```

Commit:

```bash
$ git commit
```

Commit general de cambios:

```bash
$ git commit -a
```

Status:

```bash
$ git status
```

Restituir ficheros borrados:

```bash
$ git checkout -f
```

Log:

```bash
$ git log
```

Log indicando los ficheros modificados:

```bash
$ git log --name-status
$ git log --stat
```

Rename:

```bash
$ git mv fichero.txt fichero.log
```

Preparar un servidor:

```bash
$ cd first_app/..
$ git clone --bare first_app first_app.git
$ scp -r first_app.git usuario@dominio.com:git
```

Conectar la copia de trabajo con un servidor:

```bash
$ cd first_app
$ git remote add origin usuario@dominio.com:git/first_app.git
```

(`origin` es el nombre de la conexión; puede ser cualquier cosa, aunque si se pone otra cosa habrá que especificar el nombre al hacer `push`, ya que `origin` es el nombre de destino predeterminado)

Mostrar la lista de conexiones de la copia de trabajo con servidores:

```bash
$ git remote -v
```

Desconectar la copia de trabajo con un servidor:

```bash
$ git remote rm origin
```

(`origin` es el nombre de la conexión; puede ser cualquier otro)

Checkout (remoto):

```bash
$ git clone usuario@dominio.com:git/first_app.git
```

Sincronizar con el servidor remoto:

```bash
$ git push [origin master]
```

Info (parecido a svn info):

```bash
$ cat .git/config
```

Crear un tag

```bash
$ git tag -a tag_id -m "Creación de tag tag_id."
$ git push --follow-tags
```

Eliminación de un tag

```bash
$ git tag -d tag_id
$ git push origin :refs/tags/tag_id
```

Eliminación de último commit ([Fuente](http://stackoverflow.com/questions/1338728/delete-commits-from-a-branch-in-git))

```bash
$ git reset --hard HEAD~1
```

Si el commit ya ha subido al repositorio hacer además:

```bash
git push origin HEAD --force
```

## Diff's

Distintos tipos de diff's:

* working vs staging: git diff
* staging vs snapshot: git diff --staged
* working vs snapshot: git diff HEAD
* snapshot vs snapshot: git diff <from_SHA1> <to_SHA1>

Ficheros modificados entre dos commits:

```bash
$ git diff --name-only SHA1 SHA2
$ #o
$ git diff --stat SHA1 SHA2
```

Diferencias en un fichero entre dos commits:

```bash
$ git diff SHA1 SHA2 FICHERO
```

Muestra la versión de un fichero en un determinado commit:

```bash
$ git show SHA:FILE
```

## Branches

Creación:

```bash
$ git checkout -b alta-usuarios
```

Listado de branches:

```bash
$ git branch
```

Listado de branches locales y remotos:

```bash
$ git branch -a
```

Seleccionar un branch:

```bash
$ git checkout alta-usuarios
```

Sincronizar con el servidor remoto:

```bash
$ git push origin alta-usuarios
```

Seleccionar trunk:

```bash
$ git checkout master
```

Merge:

```bash
$ git checkout master
$ git merge alta-usuarios
$ git branch -d alta-usuarios
```

Abandonar y borrar un branch local:

```bash
$ git checkout master
$ git branch -D alta-usuarios
```

Borrar un branch remoto. Si después de hacer lo anterior hacemos un git pull la rama local volverá a crearse, ya que seguía estando en el servidor. Esto podemos arreglarlo de la siguiente manera:

```bash
$ git push origin :alta-usuarios #suponiendo que la rama en el servidor se llama igual que nuestra ex-rama local
```

o

```bash
$ git push origin --delete alta-usuarios
```

Seleccionar un branch remoto ([fuente](http://git-scm.com/book/ch3-5.html#Tracking-Branches)):

```bash
$ git checkout -b fix#3413 origin/fix#3413
```
