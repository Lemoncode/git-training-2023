# Clonando el repositorio

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

Si revisamos los conceptos previos de Git, tenemos tanto una base de datos en el servidor como bases de datos en local por cada máquina de usuario que quiera trabajar con el repositorio.

## Clonando un repo existente

Partamos de que ya existe el repositorio en _Github_ y queremos bajarlo a local para poder trabajar, a este proceso se le llama _"clonado"_
¿Por qué?

- Porque nos conectamos al repositorio en remoto.
- Descargamos la base de datos con todos los _commits_ a una base de datos
  local.

Vamos a clonarnos un repositorio, la página del mismo: *https://github.com/Lemoncode/ejemplo-repo*

Si nos fijamos, pinchando en el botón _code_ podemos obtener la dirección para clonarlo via _HTTP_ o _SSH_.

La copiamos, nos vamos al terminal, y vamos a crearnos una carpeta de trabajo
dentro de esa carpeta ejecutamos el siguiente comando:

```bash
git clone https://github.com/Lemoncode/ejemplo-repo.git
```

Si nos fijamos ya tenemos el repo en nuestro disco duro, vamos a ver esto en detalle:

- Fíjate que por un lado tenemos una carpeta oculta que se llama: _.git_
  si nos metemos dentro podemos ver la _"base de datos"_ de Git que se ha creado.

- Por otro lado necesitamos mantener un vínculo con el servidor para sincronizar
  la información, para ello vemos que tenemos ramas (veremos este concepto más
  adelante) marcadas con el prefijo _origin_ y otras que no.

> Ramas: de momento nos quedamos con una explicación corta, son copias del código
> que tiene un ciclo de vida independiente y que podemos mezclarlas más adelante.

Vamos a ejecutar el siguiente comando

```bash
git branch -a
```

> Si usamos el flag _-a_ podemos ver tanto las ramas locales como remotas, si en cambio utilizamos el flag _-r_ nos muestra sólo las ramas remotas y si no ponemos flag alguno nos muestra sólo las locales.

Aquí podemos ver que tenemos lo siguiente:

```bash
main
remotes/origin/head
remotes/origin/main
```

Es decir tenemos una rama local llamada _"main"_.
Tenemos una rama remota llamada _"main"_.

Y también tenemos un _head_, esto suele coincidir con la rama
_"main"_ pero no tiene por qué, le decimos a un clon nuevo que rama
usar como cabeza local.

De esta manera tenemos sincronizado nuestra base de datos local
con la base de datos que nos podemos encontrar en el servidor.

Un tema interesante es que podemos apuntar a múltiples servidores
pero uno sólo se puede llamar _origin_, ya veremos para que puede servir
esto más adelante.

## Creando repo desde la web de Github

Si vas a arrancar un proyecto desde cero y tengo claro que lo voy a tener
desde el día cero en _Github_, podemos directamente crearlo desde la web
de _Github_ y clonarlo.

Para ello nos vamos a la web de _github_ (nos hará falta tener cuenta de usuario).

Y pulsamos sobre _new_, aquí le damos nombre al repositorio, elegimos que sea
público y es buena idea añadir en los _check_ el readme.md así tenemos un
primer _commit_ en la rama main, en caso de que no, cuando bajemos el
proyecto si hacemos un _git branch -a_ no veremos ninguna rama.

Vamos a copiar y clonarnos el repo usando _git clone_.

"_Ojo lluvia_", si seguimos trabajando aquí lo primero que tendremos que
hacer es añadir un fichero _.gitignore_ para ignorar los archivos
temporales de nuestro proyecto.
