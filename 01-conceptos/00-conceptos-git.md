# CONCEPTOS

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

# Introducción

Hace ya años atrás, quién no recuerda guardar los archivos en local y pasárselo a un compañero para que lo revisara, o bien, enviarlo por correo electrónico para su revisión.

Incluso de guardar los archivos en un disco duro externo y llevarlo a la oficina para que lo revisaran, o incluso, guardar los archivos en un servidor FTP para que los descargaran y revisaran.

También existía el problema de que un compañero tocara en un archivo que estaba trabajando otro compañero, y que al final se perdieran los cambios realizados por uno de los dos.

A mediados de los 90 y a principios de los 2000 se empezo a crear un servidor de control de versiones llamado CVS, que permitía controlar los cambios realizados en los archivos de un proyecto, de forma que se pudiera volver a versiones anteriores si fuera necesario.

Todo esto era un problema, y es que no había un sistema de control de versiones que nos permitiera controlar los cambios realizados en los archivos de un proyecto, de forma que se pudiera volver a versiones anteriores si fuese necesario.

# Sistema de versiones distribuido

En un sistema de control de versiones distribuido cada desarrollador tiene una copia completa del código. Esto permite que los desarrolladores puedan trabajar de forma independiente sin tener que estar conectados a una red.

Utilizando Forks, cada desarrollador puede tener una copia del repositorio en su propio servidor, y sincronizar los cambios con el repositorio centralizado cuando sea necesario.

De esta manera si el servidor donde se encuentra el repositorio centralizado se cae, o se corta la red eléctrica los desarrolladores pueden seguir trabajando sin problemas.

## Desventajas de un sistema de versiones distribuido

- Añadimos más complejidad.
- La curva de aprendizaje es más dura.
- Tenemos que saber muy bien qué estamos haciendo.
- Las sincronizaciones en algunos escenarios pueden ser dolorosas.

# ¿Qué es Git?

## Historia de Git

Git fue creado por **Linus Torvalds**, el creador de Linux, en 2005. En un principio, Git fue creado para el desarrollo del kernel de Linux, pero con el tiempo se ha convertido en un sistema de control de versiones muy utilizado en el desarrollo de software.

## ¿Qué se tuvo en cuenta al crear Git?

- Velocidad

- Diseño simple

- Orientado a poder tener a un equipo grande de desarrolladores trabajando en características distintas del proyecto (ramas).

- Que fuera 100% distribuido.

- Que fuera capaz de manejar grandes proyectos.

## Cómo guarda los ficheros y las carpetas Git

En repositorios clásicos no se guardaban los ficheros completos, sino que se guardaban los cambios realizados en cada fichero, de forma que sí se quería volver a una versión anterior, se tenía que ir reconstruyendo los ficheros y esto terminaba siendo ineficiente.

En Git lo que hicieron es, si el fichero no ha cambiado almaceno un puntero en el fichero anterior, y si el fichero ha cambiado almaceno el fichero completo.

Si quiero cargar una versión antigua se hace súper rápido, ya que vamos a la lista de ficheros, a los punteros, me los traigo y no tengo que estar reconstruyendo los ficheros.

## Trabajando en local

En un repositorio clásico, cuando trabajamos en local, tenemos que estar conectados a internet para poder trabajar, ya que los cambios se guardan en el servidor.

Una de las ventajas de Git es que tenemos una base de datos local para interactucar con el repositorio, y no tenemos que estar conectados a internet para trabajar.

## Otras características de Git

- **Integridad de los datos**: Git almacena los datos en formato *SHA-1*, es una cadena de 40 caracteres que se genera a partir de los datos del fichero.

- **No se borran datos**: Git no borra los datos, sino que los marca como borrados, de forma que si se quiere recuperar un fichero borrado se puede hacer.

## Funcionamiento de Git

Vamos a empezar viendo los estados de los ficheros. En Git los ficheros pueden estar en 3 estados:

- ***Untracked***: son ficheros que no están en el repositorio, y no están siendo controlados por Git. Si yo no quiero que Git controle un fichero, lo añado al fichero _.gitignore_.

- ***Unmodified***: son ficheros que están en el repositorio, pero no han sido modificados.

- ***Modified***: son ficheros que están en el repositorio, y han sido modificados. Estos ficheros no puedo hacer *commit* de ellos, ya que Git no sabe si quiero guardar los cambios o no.

- ***Staged***: son ficheros que están en el repositorio, y han sido modificados. Estos ficheros están preparados para hacer *commit*, ya que Git sabe que quiero guardar los cambios.

Si añado un fichero nuevo, ***Untracked***, con **git add** lo paso a ***Staged***.

¿Qué pasa si tengo ya un fichero que existe en el repositorio?

Si modifico el fichero, pasa a ***Modified***, si hago **git add** pasa a ***Staged***. Una vez que está en ***Staged*** puedo hacer ***git commit*** y puedo guardarlo en mi repositorio local.

Una vez que he realizado el _commit_, el fichero pasaría a ***Unmodified*** y vuelta a empezar.

## Conflictos y merge

Si en un repositorio lo toca más de una persona... nos podemos encontrar que ambas toquen en el mismo fichero e intenten subir cambios ¿Qué pasaría entonces?

Git no sabría qué hacer y nos daría un conflicto. Para solucionar este conflicto, tendríamos que decidir qué cambios queremos conservar y qué cambios queremos descartar.

## Ramas

Hasta ahora hemos estado desarrollando en un solo hilo (se llama rama _master_ o _main_), pero en un proyecto real esto puede ser problemático:

- Imagínate que tenemos una aplicación en producción, y queremos desarrollar una nueva funcionalidad. Si desarrollamos en la rama _master_ y tenemos un error, no podemos volver a la versión anterior, ya que la versión anterior no tiene la nueva funcionalidad.

- Si este desarrollo lo subo a la rama principal, ¿Qué pasa si tengo que hacer un *hotfix*? ¿Cómo puedo volver a la versión anterior?

- ¿Qué pasa si quiero revisar un trabajo antes de que vaya a la rama principal? ¿Cómo puedo hacerlo? ¿Cómo puedo volver a la versión anterior?

- O si quiero evitar conflictos de *merge* trabajando en paralelo con otra persona. ¿Cómo podría hacerlo?

Para solucionar estos problemas, Git nos permite crear ramas, de forma que podamos trabajar en paralelo sin tener que estar pendientes de lo que está haciendo el resto de personas.

## Configuración de Git

Hay una serie de comandos que (quizás) sólo usaras la primera vez que te instales Git.

\- Configurar nombre y correo (cada *commit* lleva esa información):

```bash
git config --global user.name "John Doe"
git config --global user.email "johndoe@ejemplo.com
```

\- Configurar la herramienta a utilizar para resolver conflictos de *merge*, por ejemplo _Visual Studio Code_:

```bash
git config --global diff.tool "vscode"
```

\- Configurar editor de texto para que Git interactúe (en *VSCode* funciona bien si usamos _bash editor_, si usamos _cmd(Command Prompt)_ puede que haya que introducir el _path_ completo):

```bash
git config --global core.editor "code --wait"
```

\- Cambiar el nombre de la rama principal para nuestros repositorios:

```bash
git config --global init.defaultBranch "main"
```

## Vamos a la nube

Hasta ahora hemos estado trabajando con Git en local, pero ¿Qué pasa si queremos trabajar con Git en la nube?

Lo más normal es irnos a un proveedor de servicios de Git, como por ejemplo _GitHub_, _GitLab_ o _BitBucket_. Estos proveedores nos ofrecen un servicio de almacenamiento de repositorios Git, y nos permiten trabajar en equipo de forma distribuida.

¿Por qué un proveedor especializado en la nube?

- Te quitas costes operativos (instalación, quién administra, *backups*, parches, caídas,...).

- Funcionan muy bien (están especializados en Git).

- Hay opciones baratas (0€ por usuario, 2€ por usuario..., incluso gratis para proyectos *Open Source*)

- Son potentes y escalan contigo.

- Te permiten enlazar con siguientes pasos de industrialización (CI/CD, despliegue, monitorización, ...)
