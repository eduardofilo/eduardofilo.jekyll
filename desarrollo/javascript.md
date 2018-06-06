---
layout: default
permalink: /desarrollo/javascript.html
---

# JavaScript

## JSON
La siguiente sentencia serializa en forma de JSON cualquier objeto. Es muy útil para analizar un objeto:

```javascript
alert(JSON.stringify(object));
```

## NPM
Uso básico del gestor de paquetes de [Node.js](https://www.npmjs.com/).

Para gestionar las dependencias de paquetes en un proyecto hay que generar un fichero de seguimiento llamado `package.json`. Se genera con el comando (si añadimos la opción `-y` dará todos los valores predeterminados automáticamente):

    npm init

Para descargar un paquete (por ejemplo [lodash](https://www.npmjs.com/package/lodash)) e incorporarlo al fichero `package.json` ejecutar:

    npm install lodash --save

Encontraremos que el paquete se ha descargado en un subdirectorio llamado `node_modules` e incorporado a la sección `dependencies` de `packages.json` (si no hubiéramos puesto la opción `--save` sólo se habría descargado).

Algunos comandos útiles de npm son:

* `npm install`: Descarga todos los paquetes indicados en `package.json`.
* `npm ls`: Muestra los paquetes instalados.
* `npm update`: Descarga las ultimas versiones de los paquetes instalados.
* `npm show [package]@* version`: Muestra las versiones disponibles (en el repositorio npm) del paquete indicado. Por ejemplo: `npm show lodash@* version`.