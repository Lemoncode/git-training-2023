# Introducción

<img src="../content/logo.png" width="120px">

<div style="page-break-before:always"></div>

Cuando trabajamos en un proyecto open source, es normal que se den casos
tales como que hayan cientos de colaboradores, o colaboradores que no
conocemos de nada, ¿Te imaginas gestionar permisos en estos casos?
Sería complicado y podría abrir brechas de seguridad.

Vamos a ver como funciona el "fork" de un proyecto, con un caso práctico.

# Manos a la obra

- Imaginemos que hay un grupo de voluntarios que quieren añadir al repo
  del curso de git, van a haber
  17 colaboradores, ¿Cómo podemos gestionar esto?

- A nivel de gestión, podríamos crear un _issue_ por cada fichero,
  el propio colaborador puede proponerlo (crear un _issue_).

- El colaborador puede "forkear" el repo, ¿Esto qué es?

  - Se te crea en tu area de Github un repositorio con una copia
    del repositorio original (como si fuera una fotocopia).
  - Ese repositorio apunta a dos servidores el que acabas de
    fotocopiar y el original.

- En ese proyecto tú puedes trabajar como mejor te venga (creando
  ramas, o en master, etc...).


- A la hora de hacer el _commit_ vamos a referenciar el _issue_ con el
  siguiente comentario.

```bash
git add .
```

> Cambiar 10 por el id del issue

```bash
git commit -am "closes #10"
```

> Nota puede que al estar forkeado te haga falta referenciar el repo
> completo (octo-org/octo-repo#100)

- Si ya estamos listos, puedo pedir pull request al repositorio original
  (a partir de ahora lo llamaremos al repositorio pata negra).

- En el caso del usuario forkeado no podrá mezclar la pull.

- El administrador / mantenedores del proyecto original pueden
  revisar y mezclar la rama.
