# Introducción

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

En este ejemplo vamos a empezar a trabajar con ramas.

# Manos a la obra

Vamos crear un directorio de trabajo, lo llamaremos _prueba1_

Linux / Mac OS

```bash
mkdir prueba1
cd prueba1
```

Windows

```bash
md prueba1
cd prueba1
```

Vamos a inicializar un repositorio de *git* dentro de esta carpeta:

```bash
git init
```

Vamos a crear un primer *commit* de prueba, creamos un fichero de texto con el editor que queramos:

_./readme.md_

```md
# Mi Proyecto

texto de prueba
```

Vamos a añadir el fichero y *comitearlo*:

```bash
git add .
```

```bash
git commit -am "añadiendo el readme.md"
```

> ¿Si pongo el parámetro _-a_ en el commit porque tengo que hacer el _git add_ previo? Porque este fichero es nuevo y está en estado _untracked_, el flag -a sólo añade al stage los ficheros que han sido modificados o borrados.

Si queremos asegurarnos de que todo ha salido bien:

```bash
git status
```

Vamos a meternos con las ramas, creamos una rama que vamos a llamar *ramaB*

```bash
git branch ramaB
```

Vamos a ver qué pinta tiene esto, para ello, desde la consola tenemos un comando para mostrar las ramas que tenemos en marcha:

```bash
git log --oneline --decorate --graph --all
```

El flag _--oneline_ nos muestra los *commits* en una sola línea, el flag _--decorate_ nos muestra las ramas y los *commits* a los que apuntan, el flag _--graph_ nos muestra un árbol de *commits* y el flag _--all_ nos muestra todas las ramas, no sólo la que está activa.

Aquí podemos ver que tenemos dos ramas master y *ramaB* y que *HEAD* apunta a *master* (aunque *ramaB* está apuntando al mismo *commit*)

Nos vamos a la *ramaB* y vamos a trabajar sobre ella:

```bash
git checkout ramaB
```

Vamos a hacer un *commit* sobre esa rama, creamos un fichero

_index.html_

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <h1>¡Hola Mundo!</h1>
  </body>
</html>
```

Y lo *commiteamos* de un tirón:

```bash
git add .
```

```bash
git commit -a -m "añadiendo página principal"
```

Veamos cómo van evolucionando las ramas:

```bash
git log --oneline --decorate --graph --all
```

Ahora podemos ver que tenemos dos ramas cada una va por su camino, y que *head* está ya sólo sobre la *ramaB*

Volvemos a la rama *master*:

```bash
git checkout master
```

Creamos un archivo de JavaScript, que vamos a llamar _prueba.js_ y le vamos a añadir un poco de código:

_prueba.js_

```bash
console.log("Hola desde JavaScript");
```

Y vamos hacer un *commit* sobre *master*:

```bash
git add .
```

```bash
git commit -a -m "un poco de javascript"
```

¿Cómo ha quedado la cosa? Veamos el árbol:

```bash
git log --oneline --decorate --graph --all
```

Fíjate como ahora si podemos ver una bifurcación clara de *commits* entre las dos ramas.

Aprovechamos que estamos en *master*, y nos planteamos lo siguiente: ¿Y si quisiéramos crear una rama y directamente ponerla como activa? Creemos una ramaC, esto lo podemos hacer añadiendo el parámetro _-b_.

```bash
git checkout -b ramaC
```

Vemos que en efecto la rama activa es la _ramaC_ que acabamos de crear:

```bash
git status
```

Veamos cómo queda la cosa:

```bash
git log --oneline --decorate --graph --all
```

La *ramaC* está en el mismo *commit* que *master* y la *ramaB* ya va por su camino.

Ya hemos cubierto algunos conceptos básicos, en el próximo ejemplo vamos a por *"merge"* de los fáciles :).
