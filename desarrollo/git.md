---
layout: default
permalink: /desarrollo/git.html
---

# Git

## Enlaces

*  [Libro Pro Git en español](http://git-scm.com/book/es)
*  [Cheat Sheat](http://cheat.errtheblog.com/s/git)
*  [git - la guía sencilla](http://rogerdudler.github.com/git-guide/index.es.html) :exclamation:
*  [Git Tutorials & Training by Atlassian](http://atlassian.com/git) :exclamation:

## Comandos básicos

Config:
{% highlight bash %}
git config --global user.name "Eduardo Moreno"
git config --global user.email sistemas@sanelmann.es
git config --global alias.co checkout
git config --global core.editor "subl -w"
{% endhighlight %}

Alternativamente se pueden hacer todos los cambios simultáneamente editando el fichero `~/.gitconfig`. Una configuración podría ser:

{% highlight text %}
[user]
        name = Eduardo Moreno
        email = user@dominio.com
[alias]
        co = checkout
        ci = commit
        st = status
[core]
        editor = subl -w
{% endhighlight %}

Creación repositorio (local; crea el subdirectorio `.git`):

{% highlight bash %}
cd first_app
git init
{% endhighlight %}

Add:

{% highlight bash %}
git add .
{% endhighlight %}

Commit:

{% highlight bash %}
git commit
{% endhighlight %}

Commit general de cambios:

{% highlight bash %}
git commit -a
{% endhighlight %}

Status:

{% highlight bash %}
git status
{% endhighlight %}

Restituir ficheros borrados:

{% highlight bash %}
git checkout -f
{% endhighlight %}

Log:

{% highlight bash %}
git log
{% endhighlight %}

Log indicando los ficheros modificados:

{% highlight bash %}
git log --name-status
git log --stat
{% endhighlight %}

Diferencias en ficheros entre dos commits:

{% highlight bash %}
git diff bdfe0ca0a7d69836bb9fe8da741aa7db9a041567 7c3f40a99e3f4860cf2f6327e118fd433e9ec5f6
{% endhighlight %}

Rename:

{% highlight bash %}
git mv fichero.txt fichero.log
{% endhighlight %}

Preparar un servidor:

{% highlight bash %}
cd first_app/..
git clone --bare first_app first_app.git
scp -r first_app.git tecnoemporium@tecnoemporium.es:git
{% endhighlight %}

Conectar la copia de trabajo con un servidor:

{% highlight bash %}
cd first_app
git remote add origin tecnoemporium@tecnoemporium.es:git/first_app.git
{% endhighlight %}

(`origin` es el nombre de la conexión; puede ser cualquier cosa, aunque si se pone otra cosa habrá que especificar el nombre al hacer `push`, ya que `origin` es el nombre de destino predeterminado)

Mostrar la lista de conexiones de la copia de trabajo con servidores:

{% highlight bash %}
git remote -v
{% endhighlight %}

Desconectar la copia de trabajo con un servidor:

{% highlight bash %}
git remote rm origin
{% endhighlight %}

(`origin` es el nombre de la conexión; puede ser cualquier otro)

Checkout (remoto):

{% highlight bash %}
git clone tecnoemporium@tecnoemporium.es:git/first_app.git
{% endhighlight %}

Sincronizar con el servidor remoto:

{% highlight bash %}
git push [origin master]
{% endhighlight %}

Info (parecido a svn info):

{% highlight bash %}
cat .git/config
{% endhighlight %}

Ficheros modificados entre dos commits:

{% highlight bash %}
git diff --name-only SHA1 SHA2
#o
git diff --stat SHA1 SHA2
{% endhighlight %}

Diferencias en un fichero entre dos commits:

{% highlight bash %}
git diff SHA1 SHA2 FICHERO
{% endhighlight %}

Muestra la versión de un fichero en un determinado commit:

{% highlight bash %}
git show SHA:FILE
{% endhighlight %}

## Branches

Creación:

{% highlight bash %}
git checkout -b alta-usuarios
{% endhighlight %}

Listado de branches:

{% highlight bash %}
git branch
{% endhighlight %}

Listado de branches locales y remotos:

{% highlight bash %}
git branch -a
{% endhighlight %}

Seleccionar un branch:

{% highlight bash %}
git checkout alta-usuarios
{% endhighlight %}

Sincronizar con el servidor remoto:

{% highlight bash %}
git push origin alta-usuarios
{% endhighlight %}

Seleccionar trunk:

{% highlight bash %}
git checkout master
{% endhighlight %}

Merge:

{% highlight bash %}
git checkout master
git merge alta-usuarios
git branch -d alta-usuarios
{% endhighlight %}

Abandonar un branch:

{% highlight bash %}
git checkout master
git branch -D alta-usuarios
{% endhighlight %}

Seleccionar un branch remoto ([fuente](http://git-scm.com/book/ch3-5.html#Tracking-Branches)):

{% highlight bash %}
git checkout -b fix#3413 origin/fix#3413
{% endhighlight %}
