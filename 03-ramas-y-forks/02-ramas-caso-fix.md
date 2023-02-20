# Introducción

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

Crear ramas está muy bien, pero en algún momento tendremos que mezclarlas... en este ejemplo vamos a simular un caso real con dos "casos felices de *merge*".

# Manos a la obra

Vamos a crear un directorio de trabajo, lo llamaremos _prueba2_.

*Linux / Mac OS*

```bash
mkdir prueba2
cd prueba2
```

*Windows*

```bash
md prueba2
cd prueba2
```

Vamos a inicializar un repositorio de *git* dentro de esta carpeta:

```bash
git init
```

Vamos a crear un par de *commits* sobre *master* (lo vamos a hacer fichero a fichero, esto no tiene por qué ser así, podríamos haber creado los dos ficheros y directamente añadirlos en un *commit*)

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

Vamos a hacer un segundo *commit* sobre *master*, creamos un fichero

_index.html_

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <h1>¡ Hola Mundo !</h1>
  </body>
</html>
```

Y lo *commiteamos*:

```bash
git add .
```

```bash
git commit -a -m "añadiendo página principal"
```

Todo bien, salimos a producción y dejamos el corte de código que hay en producción en la rama *master*, pero mientras necesitamos seguir implementando nuevas características, así que vamos al lio.

Nos creamos una rama para implementar nuestro caso.

```bash
git branch caso1
```

```bash
git checkout caso1
```

Vamos a ir añadiendo una segunda página a nuestro repositorio

_./prueba.html_

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <h1>Soy la página B</h1>
  </body>
</html>
```

```bash
git add .
```

```bash
git commit -am "nueva pagina"
```

De repente nos llaman y nos dicen que ha habido un "fuego", hay un error crítico que tenemos que arreglar en la página que hay en producción, nos toca ponernos el gorro de bombero pasarnos a master y arremangarnos, lo bueno es que el trabajo en la *ramaB* se queda como está (si no hubiéramos hecho *commit* tendríamos que hacerlo, o tirar para atrás los cambios o meterlo en *stash*).

Vamos a pasarnos a master y nos arremangamos

```bash
git checkout master
```

Vamos a ser ordenados para arreglar el parche creamos una rama que llamaremos "parche" (no es muy original el nombre ni descriptivo, en el mundo real busca nombres que ayuden a identificar la rama), y vamos a parchear la aplicación:

```bash
git checkout -b parche
```

_index.html_

```diff
<!DOCTYPE html>
<html lang="en">
  <body>
-    <h1>¡ Hola Mundo !</h1>
+    <h1>¡ Hola Git !</h1>
  </body>
</html>
```

Y vamos a hacer *commit* del cambio, esta vez no me hace falta hacer un _add_ porque el fichero está *trackeado* (hemos realizado una modificación).

```bash
git commit -am "ñapa aplicada"
```

Vamos a ver qué pinta va teniendo esto:

```bash
git log --oneline --decorate --graph --all
```

Siguiente paso vamos a *master* y mezclamos la rama de parche en *master*:

```bash
git checkout master
```

```bash
git merge parche
```

Si te fijas en este *merge* pone *"fast forward"*, si vemos como están las ramas lo entenderemos:

```bash
git log --oneline --decorate --graph --all
```

El *commit* anterior de master era justo el consecutivo de la *ramaB* así que sólo hace falta mover el puntero.

Volvemos a nuestra rama *caso1*

```bash
git checkout caso1
```

Añadimos un nuevo fichero

_./business.js_

```js
console.log("Hello from business");
```

Lo añadimos y *commiteamos*:

```bash
git add .
```

```bash
git commit -a -m "Caso completo"
```

Vamos a mezclar el caso en *master*:

```bash
git checkout master
```

```bash
git merge caso1 -m "mezclado caso1"
```

Fíjate que aquí no se puede aplicar un *fast forward merge*, porque el *commit* que creamos no es el directo de la rama
a la que vamos a mezclar.

Vamos a ver cómo han quedado las ramas

```bash
git log --oneline --decorate --graph --all
```
