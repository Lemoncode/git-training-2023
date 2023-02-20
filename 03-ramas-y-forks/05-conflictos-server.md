# Introducción

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

Hasta ahora hemos estado trabajando en un repositorio local, vamos
a ver cómo manejar conflictos si estamos conectado a un repositorio
en la nube.

# Pasos

Arrancamos con nuestro proyecto:

Vamos a crear una carpeta, podemos llamarla _practica_

```bash
mkdir practica
```

```bash
cd practica
```

Vamos a inicializar nuestro proyecto de Git:

```bash
git init
```

Y creamos dos ficheros:

_ficheroa.js_

```js
console.log("*****************");
console.log("soy el fichero a");
console.log("*****************");
```

_ficherob.js_

```js
console.log("*****************");
console.log("soy el fichero b");
console.log("*****************");
```

Vamos a _comitear_ esto en local en la rama master:

```bash
git add .
```

```bash
git commit -m "ficheros iniciales"
```

Antes de seguir vamos a conectar esto con un repo en Github,
para ello:

- Creamos el proyecto en Github.
- Copiamos la url (depende de si estás con https o ssh) para
  clonar

Vamos añadirlo como _origin_ a nuestro repo:

```bash
git remote add origin https://github.com/...
```

```bash
git push --set-upstream origin master
```

Ya tenemos el repo conectado (navegamos al portal
de github y en efecto vemos que todo se ha subido)

Vamos ahora a replicar el _issue_ del conflicto.

Nos creamos una rama nueva en local:

```bash
git branch mirama
```

```bash
git checkout mirama
```

_ficheroa.js_

```diff
- console.log("*****************");
+ console.log("+++++++++++++++++");
console.log("soy el fichero a");
- console.log("*****************");
+ console.log("+++++++++++++++++");
```

_ficherob.js_

```diff
- console.log("*****************");
+ console.log("-----------------");
- console.log("soy el fichero b");
+ console.log("soy el segundo fichero");
- console.log("*****************");
+ console.log("-----------------");
```

Vamos a subir los cambios

```bash
git commit -am "actualizacion contenido"
```

Si queremos podemos subirlo a servidor

```bash
git push -u origin mirama
```

Ahora cambiamos a la rama master

```bash
git checkout master
```

Y modificamos el fichero _ficherob.js_

_ficherob.js_

```diff
console.log("*****************");
- console.log("soy el fichero b");
+ console.log("fichero II");
console.log("*****************");
```

Y hacemos _commit_ del cambio:

```bash
git commit -am "actualizacion segundo fichero"
```

y subo lo cambios a servidor

```bash
git push
```

Queremos mezclar los cambios de mi rama a master, lo primero que
hago es saltar a master, mezclo con mi rama y vemos que tenemos conflictos

```bash
git merge mirama -m "mezclando mirama"
```

Vemos que tenemos el conflicto, lo arreglamos.

Ya estamos listos para comitear:

```bash
git commit -am "mezclando mi rama"
```

Y subir los cambios a servidor

```bash
git push
```

# Git Pull vs Fetch

_Git pull_ se baja cambios y modifica tu corte en local (puede
lanzar un _merge_ en tu rama en _checkout_), esto suele ser lo normal que tú necesitas (git pull lo que hace es un fetch y una acción adicional, normalmente un merge)

_Git fetch_, se baja los cambios de tu remoto, pero no hace
cambios en tu local (es decir actualiza las ramas remotas, pero
las locales enlazadas se quedan como está).

[Más información](https://www.gitkraken.com/learn/git/problems/git-pull-vs-fetch)

[En español](https://geekytheory.com/diferencia-entre-git-pull-y-git-fetch/)

[Git Fetch en detalle](https://www.atlassian.com/es/git/tutorials/syncing/git-fetch)

[Git Pull en detalle](https://www.atlassian.com/es/git/tutorials/syncing/git-pull)
