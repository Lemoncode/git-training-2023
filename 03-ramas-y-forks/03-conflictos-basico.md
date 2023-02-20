# Introducción

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

En este ejemplo vamos a crear una rama y generar un conflicto de _merge_, y veremos qué podemos hacer para solucionarlo.

# Manos a la obra

Vamos a crear una carpeta, la podemos llamar _miproyecto_

```bash
mkdir miproyecto
```

```bash
cd miproyecto
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

Ahora creamos una rama que llamaremos _cambiostexto_, vamos
a cambiar el ficheroA y el ficheroB:

```bash
git branch cambiostexto
```

```bash
git checkout cambiostexto
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

Esto estaría para hacer un _merge_ limpio (no hay habido ningún _commit_
intermedio entre esta rama y main), pero en el mundo real, esto
no tiene por qué pasar hay más personas trabajando en el proyecto, vamos
a simular que otra persona ha estado trabajando en máster y ha introducido
cambios que pueden romper:

```bash
git checkout master
```

Vamos a editar el segundo fichero:

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

> PASO AQUI copiar el proyecto a tres carpetas, la original, la pechoromano y la mergetool

¿Qué pasa si ahora intentamos mezclar de la rama _cambiostexto_ a la rama _master_?

```bash
git merge cambiostexto
```

Aquí nos dice que no puede mezclar de forma automática ya que hay conflictos de _merge_,
y tenemos que ser nosotros los que decidamos que hacer, toca resolver o tirar para átras
para poder seguir trabajando.

Vamos a ver dónde está el lio:

```bash
git status
```

Todo lo que tiene conflictos de _merge_ lo podrás encontrar en la lista como _unmerged_.

¿Cómo podemos resolver estos conflictos?

- A modo "pecho romano" y es abriendo los ficheros y a mano ir eligiendo la opción
  que más nos cuadre.
- Utilizando alguna _tool_ de _merge_ como KDiff, WinMerge, Visual Studio Code...

Vamos a hacer una copia del proyecto y jugar con ambas opciones (creamos tres copias, la original,
la pechoromano y la mergetool).

## Modo pecho romano

Veamos como marca los conflictos en los ficheros Git, si abrimos _ficherob.js_, podemos
ver lo siguiente (desde terminal _cat ficherob.js_):

```js
<<<<<<< HEAD
console.log("*****************");
console.log("soy el fichero II");
console.log("*****************");
=======
console.log("-----------------");
console.log("soy el segundo fichero");
console.log("-----------------");
>>>>>>> cambiostexto
```

Podríamos directamente elegir que la segunda opción es la que se queda cargarnos lo que toque y eliminar las marcas de git.

Una vez que lo tuviéramos todo resuelto añadiremos los ficheros a _staging_, y después
haríamos un _commit_ con el _merge_ resuelto.

```bash
git add .
```

```bash
git commit -am "Merge resuelto"
```

Ahora vamos a borrar la rama _cambiostexto_ no sin antes jugar un poco:

Cambiamos a la rama _cambiostexto_

```bash
git checkout cambiostexto
```

Borramos la rama

```bash
git branch -d cambiostexto
```

Upa esto nos da un mensaje de error ¿Por qué? ... en efecto no puede borrar una rama si es la rama activa.

Vamos a volver a la rama _master_ y vamos a borrarlo

```bash
git checkout master
```

```bash
git branch -d cambiostexto
```

Si ahora listamos las ramas podemos ver que sólo tenemos máster:

```bash
git branch
```

## Modo Tool (Kdiff)

Otra opción es usar una herramienta de _merge_ con interfaz de usuario, para ello podemos
cambiar de carpeta y trabajar con la copia _mergetool_.

```bash
cd mergetool
```

```bash
git mergetool
```

Vamos a jugar con KDiff, se abre y vemos cuatro ventanas, vamos primero a comprender esto volvemos a kdiff y VSCode:

- Vemos los ficheros temporales que se crean.
- Trabajamos con KDiff resolviendo _issues_ y navegando por _merge_.
- Grabamos y vemos que se queda un fichero de backup con extensión _orig_ es un backup,
  comentar que se puede configurar la _diff tool_ para que no se cree.

Si no tienes _tool_ de _merge_ instalada o la que hay no te convence, en estos enlaces
hay varias

- Linux: https://www.tecmint.com/best-linux-file-diff-tools-comparison/
- Mac Os: https://coderwall.com/p/3wuuda/set-diffmerge-as-default-merge-tool-in-os-x
- Windows: https://www.git-tower.com/blog/diff-tools-windows/

Algunas Kdiff, VSCode, p4Merge...

Y por ejemplo como configurar kdiff

http://kdiff3.sourceforge.net/

- Instalar Kdiff, puedes decargarlo [aquí](https://sourceforge.net/projects/kdiff3/files/latest/download)
- Abrir el terminal y ejecutar los siguientes comandos:

```bash
git config --global --add merge.tool kdiff3
&&
git config --global --add mergetool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
&&
git config --global --add mergetool.kdiff3.trustExitCode false
&&
git config --global --add diff.guitool kdiff3
&&
git config --global --add difftool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
&&
git config --global --add difftool.kdiff3.trustExitCode false
```

Configurar Kdiff en Mac:

- Instalar Kdiff, puedes descargarlo [aquí](https://sourceforge.net/projects/kdiff3/files/latest/download)
- Abrir el terminal y ejecutar los siguientes comandos:

```bash
git config --global --add merge.tool kdiff3
&&
git config --global --add mergetool.kdiff3.path "Applications/kdiff3.app/Contents/MacOS/kdiff3"
&&
git config --global --add mergetool.kdiff3.trustExitCode false
&&
git config --global --add diff.guitool kdiff3
&&
git config --global --add difftool.kdiff3.path "Applications/kdiff3.app/Contents/MacOS/kdiff3"
&&
git config --global --add difftool.kdiff3.trustExitCode false
```

## Modo Tool (VSCode)

Veamos VSCode, saltamos a la carpeta que nos queda y ejecutamos el comando de merge

```
git merge cambiostexto
```

Ahora podemos:

- O bien ir a la lista de ficheros standard e ir corrigiendo los ficheros en rojo.
- O bien ir a la pestaña de Git y trabajar con los ficheros de la sección (merge changes).

¿Qué podemos hacer aquí?

- Podemos aceptar el cambio que hay en máster (current change).
- Aceptar el cambio que viene de la rama _cambiostexto_ (la que queremos mezclar).
- Aceptar los dos cambios
- También podríamos aceptar y editar manualmente o modificar.

Ahora que está resuelto preparamos el commit y a grabar:

```bash
git commit -am "merge resuelto"
```

> En los siguientes módulos profundizaremos en cómo funciona el tooling de VSCode para manejarnos con Git.


