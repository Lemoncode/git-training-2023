# Creando el repositorio en local
<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

## Introducción

Cuando pensamos un repositorio de código fuente se nos viene a la cabeza
un servidor al que nos conectamos y con el que interactuamos para bajar o
subir ficheros.

_Git_ es un repositorio distribuido,... ¿Qué ganamos con tenerlo instalado en nuestra máquina?:

- Podemos tener un control de versiones y poder volver atrás si hace falta
  o descartar cambios sin miedo a perderlo todo.

- Lo tenemos ya preparado para subir a un repositorio a la nube.

## Pasos

Vamos a arrancar instalando _Git_ en nuestra máquina, para ello
podemos instalarlo de esta _url_: *https://git-scm.com/downloads*

- Partimos de un proyecto web simple, lo puedes encontrar dentro de la carpeta *2 - Git* en *00-boilerplate*, vamos a copiarlo a otra carpeta de mi disco duro, lo podemos llamar _miprueba_.

- Aunque esto no está directamente relacionado con Git, vamos a instalar
  las dependencias del proyecto y ejecutarlo:

```bash
cd miprueba
```

```bash
npm install
```

```bash
npm start
```

- Bien tenemos un proyecto simple web en ejecución, vamos a ver los ficheros
  y carpetas que tenemos

```
node_modules
index.html
index.js
...
```

Si te fijas _node_modules_ es una carpeta temporal, que no debemos de subir
al repositorio (el resto sí), antes de iniciar nuestro repo, vamos a añadir
un fichero que llamaremos _.gitignore_ en nuestro raíz (muy importante que
el nombre sea ese, incluyendo el punto), en este fichero vamos a indicarle
que ignore la carpeta _node_modules_, la carpeta _.parcel-cache_ y la carpeta _dist_ y el fichero _package-lock.json_:

_.gitignore_

```
node_modules
.parcel-cache
dist
package-lock.json
```

> El fichero .gitignore soporta una serie de patrones, lo veremos
> más adelante en el curso, más info: https://git-scm.com/docs/gitignore

De esta forma evitaremos subir ficheros no deseados a nuestro repositorio.

- Vamos ahora a empezar a trabajar con _git_ en local, lo primero que hacemos
  es inicializar nuestro repo en local, para ello vamos al terminal:

```bash
git init
```

- Ahora queremos guardar en la base de datos de _git_ nuestro código,
  en Git trabajamos en dos fases, primero pasamos los ficheros a un
  paso que llaman _"staging"_ y después de _"staging"_ lo comiteamos a la
  base de datos en local:

Añadimos todos los ficheros a fase _stage_ (esto lo hacemos con el comodín .)

```bash
git add .
```

Y ahora vamos comitearlo en nuestra base de datos en local, añadimos
también un mensaje de _commit_:

```bash
git commit -m "hola git"
```

Genial ya tenemos el código subido, ahora vamos a ver como subirlo a un
repositorio en la nube (usaremos github como ejemplo).
