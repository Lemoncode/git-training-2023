# De local a la nube

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

Una vez que ya tenemos nuestra clave SSH, hemos clonado el repositorio y hemos probado que todo funciona correctamente. Vamos a ver como subir los cambios que hicimos en local a la nube.

# Preparativos

Para ello vamos a crear un repositorio en la nube, en este caso vamos a usar Github, pero podríamos usar cualquier otro servicio de repositorio remoto.

Ahora que ya tenemos nuestro repositorio y nuestro acceso al mismo desde nuestra máquina local establecido, toca interactuar con el repositorio...

Partimos del código que creamos en local, vamos a conectarlo con el repositorio a la nube y enviar cambios...

# Manos a la obra

Tenemos nuestro repositorio creado en local, vamos ahora a conectarlo con el que hemos creado en la nube, para ello nos vamos al terminal
(en la carpeta en la que lo hemos creado), y le añadimos como _origin_
remoto la _url_ del repo en la nube.

```bash
git remote add origin git@....
```

Ahora que lo hemos añadido sólo tenemos que subir la rama local que tenemos
al repo

> Nota ver si es master o main

```bash
git push -u origin master
```
