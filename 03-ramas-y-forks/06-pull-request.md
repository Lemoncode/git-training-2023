# Introducción

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

Mezclar ramas directamente desde terminal puede ser algo peligroso,
ya que hay veces en las que perdemos control sobre el código
que se está mezclando.

Vamos a ver el concepto de _Pull Request_, esta funcionalidad la implementan
prácticamente la totalidad de _DVCS_ que hay en la nube (Gitlab, Github,
Bitbucket, Azure Devops...)

# Manos a la obra

Sobre el repositorio que creamos previamente vamos a crear una nueva
rama

> Previo, nos aseguramos que estamos en máster y hacemos un pull

Vamos a crear una rama

```bash
git branch otrarama
```

```bash
git checkout otrarama
```

Vamos eliminar el _ficheroa.js_:

Vamos a insertar un nuevo fichero, _ficheroc.js_

_./ficheroc.js_

```js
console.log("fichero c");
console.log("***********");
```

Y vamos a modificar el _ficherob_:

_./ficherob.js_

```diff
console.log("*****************");
console.log("fichero II");
console.log("*****************");
+ console.log(`
+ Entre los pecados mayores que los hombres cometen, 
+ aunque algunos dicen que es la soberbia, yo digo que es el 
+ desagradecimiento
+ `)
```

Y vamos a _comitear_ los cambios:

```bash
git add .
```

```bash
git commit -am "actualizaciones"
```

```bash
git push -u origin otrarama
```

Ahora en vez de mezclar la rama desde el terminal, vámonos al portal de _github_:

Abrimos una _pull request_ de la nueva rama a _master_.

Ahora puedo ver todos los cambios que se han hecho, revisarlos y comentar mejoras.

Aquí es importante, la idea es que el revisor no cambie código, si no qué indique si se puede mejorar o si tiene dudas sobe el código que se ha escrito. El dueño de la rama es quién debe aplicar los cambios si aplican, así el desarrollador aprende.

# Conflictos...

Un tema muy interesante es el del manejo de conflictos, si los hay,
en una PR, lo que debemos de hacer es tener siempre nuestra rama actualizada con el último corte de master, es decir, mezclar master a la rama que tenemos en PR.

Como práctica podemos simular conflictos y ver como se ve en la PR.

Otro tema muy interesante es que podemos meter _checks_ en las _pull_:

- Podemos poner que sólo ciertos usuarios tengan permisos para aprobar y
  mezclar a _master_.
- Podemos obligar a que una serie de revisores hayan aprobado la _pull_.
- Podemos meter pasos previos a la _pull_ en la que automáticamente
  se lance una _build_ o _tests_ y si no pasan que no se pueda hacer _merge_.
