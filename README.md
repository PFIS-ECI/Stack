
# Stack

Stack es una herramienta multiplataforma para el desarrollo de proyectos
escritos en el lenguaje de programación Haskell.

Para instalarla siga los pasos que se encuentran en [https://docs.haskellstack.org/en/stable/README/](https://docs.haskellstack.org/en/stable/README/)

Este instructivo esta pensado para un sistema operativo linux con una
terminal en `bash`.

## PATH

La variable de entorno `PATH` se utiliza para establecer las rutas o directorios
donde se encuentran las aplicaciones a ejecutar en la linea de comandos de una
terminal. Las rutas son separadas por `:`.

Para ver su valor puede ejecutar el siguiente comando en una terminal:
```
$ echo $PATH
```

Una vez instalada la herramienta `stack` hay que agregar la ruta `~/.local/bin`
al `PATH`, donde se instalan los comandos y aplicaciones creadas por stack.

Para ello ejecutamos el siguiente comando en la terminal:

```bash
$ echo PATH="./.local/bin:$PATH" >> ~/.bashrc
```

Abrir una nueva terminal y verificar que se agrego la ruta `./.local/bin` al `PATH`:
```
$ echo $PATH
```

## Hello

Cree un directorio de trabajo y cambie su ruta actual al nuevo directorio.
En este documento se utilizará `WorkspaceHS`.

```bash
$ mkdir WorkspaceHS
$ cd WorkspaceHS
```

Cree un nuevo proyecto `stack` llamado `Hello`:

```bash
$ stack new Hello
$ cd Hello
$ stack setup
$ stack build
$ stack exec Hello-exe
```

* El comando `stack new` crea un nuevo proyecto junto con los archivos
  necesarios para ejecutarlo.
* El comando `stack setup` descarga el compilador (de ser necesario) que utiliza
  el proyecto en un lugar aislado (`~/.stack`). Para ver información de las
  rutas que utiliza el comando `stack` utilize `stack path`.
* El comando `stack build` construye el proyecto.
* El comando `stack exec` ejecuta el ejecutable del proyecto construido.
* Para instalar un ejecutable (haskell) utilizando `stack` se hace mediante el
  comando `stack install <nombre del paquete>`.

## Directorios del Proyecto

Los directorios que crea el comando `stack new` ejecutado anteriormente son los
siguientes:

```
.
├── app
│   └── Main.hs
├── ChangeLog.md
├── Hello.cabal
├── LICENSE
├── package.yaml
├── README.md
├── Setup.hs
├── src
│   └── Lib.hs
├── stack.yaml
└── test
    └── Spec.hs
```

* El directorio `app` se utiliza para los archivos relacionados con la
  construcción de ejecutables.
* El código fuente del proyecto se encuentra en el directorio `src`.
* En el directorio `test` se localizan las pruebas del proyecto.

La herramienta `stack` fue diseñada para manejar proyectos mientras que la
herramienta `cabal` es utilizada para construir paquetes.

### Paquete

Un paquete contiene por lo menos:
* un nombre y una versión
* 0 o una libreria
* 0 o mas ejecutables
* Un archivo `cabal` que describe su construcción.

La descripción de la construcción del paquete se encuentra en el archivo con
extensión `.cabal`.

### Proyecto

La herramienta `stack` esta construida sobre `cabal` y define el concepto de
proyecto. Un proyecto `stack` consta de:

* Un _resolver_ que es el conjunto de librerias (con sus respectivas versiones)
  que utiliza el proyecto.
* Dependencias adicionales que no se encuentran en el _resolver_.
* 0 o mas paquetes cabal locales.
* Configuraciones de GHC

La descripción de la construcción del proyecto se encuentra en el archivo
`stack.yaml`.

El archivo `package.yaml` utiliza el formato [`hpack`](https://github.com/sol/hpack#readme) y es una alternativa a
cabal para la descripción de los paquetes soportada por la herramienta `stack` y
realiza los cambios necesarios tanto en el archivo `package.yaml` como en el
archivo `Hello.cabal`.


## Hello Haskell

Revise el archivo `Hello.cabal` en la sección `library` - `exposed-modules`.

Edite el archivo `src/Lib.hs` para que quede:

```haskell
module Hello
    ( hello
    ) where

hello :: IO ()
hello = putStrLn "Hello Haskell"
```

Note que se renombro la función `someFunc` por la función `hello`. 

Ejecute en la terminal el comando:
```bash
$ stack build
```

A partir del error obtenido, que condición tienen los nombres de los módulos?
Arregle el nombre del archivo utilizando el comando:

```bash
$ mv src/Lib.hs src/Hello.hs
```

intente construir el proyecto y corrija los errores que se vayan presentando hasta
que logre construirlo.

Revise el archivo `Hello.cabal` en la sección `library` - `exposed-modules`.

Ejecute el proyecto:
```bash
$ stack exec Hello-exe
```

Ejecute el repl:
```bash
$ stack ghci
```

Ejecute `hello` desde el repl:
```bash
> hello
```

