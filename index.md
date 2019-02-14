---
title: Introducción a Git
separator: '^\r?\n---\r?\n$'
verticalSeparator: '^\r?\n--\r?\n$'
author: Alfredo Sánchez Alberca
theme: black
customTheme : custom
highlightTheme: "Monokai"
# css: css/custom.css,css
revealOptions:
    transition: convex
    center: true
logoImg: "https://github.com/asalber/asalber.github.io/raw/master/images/logo-git.png"
---

# Introducción a GIT

### Sistema de control de versiones

Autor [Alfredo Sánchez Alberca](http://aprendeconalf.es)

<img width="178" height="238" data-src="/img/logo-git.png" alt="Logo de Git">

---

## ¿Qué es un sistema de control de versiones?

> Un **Sistema de Control de Versiones** (SCV) es una aplicación que permite gestionar los cambios que se realizan sobre los elementos de un proyecto o repositorio, guardando así versiones del mismo en todas sus fases de desarrollo.

- Registra cada cambio en el proyecto o repositorio, quién y cuándo lo hace, en una base de datos.
- Permite volver a estados previos del desarrollo.
- Permite gestionar diferentes versiones del proyecto (ramas) para trabajar en paralelo y luego fundirlas.
- Permite colaborar entre diferentes usuarios en un mismo repositorio, facilitando la resolución de conflictos.
- Se utiliza principalmente en proyectos de desarrollo de software, pero sirve para cualquier otro tipo de proyecto.

---

## ¿Qué es Git?

**Git** es un sistema de control de versiones de código abierto ideado por Linus Torvalds (el padre del sistema operativo Linux) y actualmente es el sistema de control de versiones más extendido.

A diferencia de otros SCV Git tiene una arquitectura _distribuida_, lo que significa que en lugar de guardar todos los cambios de un proyecto en un único sitio, cada usuario contiene una copia del repositorio con el historial de cambios completo del proyecto. Esto aumenta significativamente su rendimiento.

<img width="178" height="238" data-src="/img/logo-git.png" alt="Logo de Git">

--

## ¿Qué es GitHub?

Git permite gestionar repositorios locales y también remotos, y de hecho es habitual, como medida de seguridad, mantener una copia de un repositorio local en un servidor remoto.

**GitHub** es el proveedor de alojamiento en la nube para repositorios gestionados con git más usado y el que actualmente tiene alojados más proyectos de desarrollo de software de código abierto en el mundo.

La principal ventaja de GitHub es que permite albergar un número ilimitado de repositorios tanto públicos como privados, y que además ofrece servicios de registro de errores, solicitud de nuevas funcionalidades, gestión de tareas, wikis o publicación de páginas web, para cada proyecto, incluso con el plan básico que es gratuito.

<img height="100" data-src="/img/logo-github.png" alt="Logo de GitHub"><img height="150" data-src="/img/logo-octocat.png" alt="Logo de GitHub">

---

## Configuración de Git

#### `git config`
<span></span>

- Establecer el nombre de usuario
```sh
echo $EDITOR
git config --global user.name "Your-Full-Name"
```
- Establecer el correo del usuario
```sh
git config --global user.email "your-email-address"
```
- Activar el coloreado de la salida
```sh
git config --global color.ui auto
```
- Mostrar el estado original en los conflictos
```sh
git config --global merge.conflictstyle diff3
```
- Mostrar la configuración
```sh
git config --list
```

---

## Creación de repositorios

#### `git init`

Para crear un repositorio hay que situarse dentro de la carpeta que contienen el proyecto y utilizar el comando `git init`.

Este comando crea dentro de la carpeta del proyecto otra carpeta oculta llamada `.git` que contiene la base de datos donde registrar los cambios en el repositorio.

---

## Añadir cambios a un repositorio

Con Git, cualquier cambio que hagamos en un proyecto tiene que pasar por tres estados hasta que guarde definitivamente en el repositorio.

- **Directorio de trabajo** Es el directorio que contiene todos los ficheros del proyecto, tanto si están registrados en el repositorio como si no.
- **Zona temporal de intercambio** (staging area) es una zona donde se guardan los cambios temporalmente desde el directorio de trabajo antes de hacerlos definitivos y registrarlos en el repositorio.
- **Repositorio** Es donde finalmente se guardan los cambios definitivos desde la zona temporal de intercambio.

--

### Añadir cambios a la zona de intercambio temporal
#### `git add`

- Para añadir los cambios en un fichero en el directorio de trabajo a la zona de intercambio temporal se utiliza el comando `git add <fichero>`
- Se pueden añadir los cambios de varios ficheros a la vez o incluso de una carpeta entera indicando el nombre y la ruta de la carpeta.
- Se pueden añadir todos los cambios de todos los ficheros no guardados aún con el comando `git add .`.

--

### Añadir cambios al repositorio
#### `git commit`

- Para añadir al repositorio los cambios finales desde la zona temporal de intercambio se utiliza el comando `git commit -m "mensaje"`, donde `"mensaje"` es un breve mensaje describiendo los cambios realizados que se asociará al estado actual del repositorio.

--

<img data-src="/img/git-add-commit.png" alt="Logo de Git">

---

## Registro de cambios

Para guardar los cambios en un repositorio Git utiliza una estructura de tres niveles:

- **Commit** Contiene información sobre el autor, el momento y el mensaje de los cambios.  
- **Árbol (tree)** Cada commit contiene además un árbol donde se registran los nombres y rutas de los ficheros en el repositorio cuando se hizo el commit. 
- **Blob (binary file object)** Para cada uno de los ficheros listados en el árbol hay un blob, que contiene una instantánea comprimida del contenido del fichero cuando se hizo el commit.  
Si un fichero del repositorio no ha cambiado en el commit, el árbol apunta al blob del fichero del último commit donde el fichero cambió.

--

## Referenciar un commit

Cada commit tiene asociado un código hash de 40 dígitos que lo identifica de manera única. 
Hay dos formas de referirse a un commit: 
- Nombre absoluto: Se utiliza su código hash (basta indicar los 4 o 5 primeros dígitos).
- Nombre relativo: Se utiliza la palabra `HEAD` para referirse siempre al último commit. Para referirse al penúltimo commit se utiliza `HEAD~1`, al antepenúltimo `HEAD~2`, etc.

--

<img data-src="/img/modelo-datos-git.png" alt="Modelo de datos de Git">

---

## Consultar el estado de un repositorio
#### `git status`

Para consultar el estado de los cambios en cada momento se utiliza el comando `git status`.

Este comando muestra los ficheros con cambios en el directorio de trabajo que no se han añadido a la zona de intercambio temporal y los ficheros en la zona de intercambio temporal que no se han añadido al repositorio.

---

## Mostrar las diferencias entre versiones
#### `git diff`

- `git diff` muestra las diferencias entre el directorio de trabajo y la zona de intercambio temporal.
- `git diff --cached` muestra las diferencias entre la zona de intercambio temporal y el último commit.
- `git diff HEAD` muestra la diferencia entre el directorio de trabajo y el último commit.

---

## Mostrar un los datos de un commit
#### `git show`

- `git show` muestra el usuario, el día, la hora y el mensaje del último commit, así como las diferencias con el anterior.
- `git show <commit>` muestra el usuario, el día, la hora y el mensaje del commit indicado, así como las diferencias con el anterior.

---

## Mostrar el historial de commits de un repositorio
#### `git log`

`git log` muestra el historial de commits de un respositorio ordenado cronológicamente. Para cada commit muestra su código hash, el autor, la fecha, la hora y el mensaje asociado.