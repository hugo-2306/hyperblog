# Curso Profesional de Git y Github

## ¿Qué es staging, repositorios y cuál es el ciclo básico de trabajo en GitHub?

Para iniciar un repositorio, o sea, activar el sistema de control de versiones de Git en tu proyecto, solo debes ejecutar el comando: git init (git espacio init) desde la terminal situado en el directorio de tu proyecto.

Este comando se encargará de dos cosas: primero, crear una carpeta .git donde se guardará toda la base de datos con _cambios atómicos_ de nuestro proyecto; y segundo, crear un área en la memoria RAM, que conocemos como Staging, que guardará temporalmente nuestros archivos (cuando ejecutemos un comando especial para eso) y nos permitirá, más adelante, guardar estos cambios en el repositorio (también con un comando especial).

**Ciclo de vida o estados de los archivos en Git:**

Cuando trabajamos con Git, nuestros archivos pueden vivir y moverse entre 4 diferentes estados (cuando trabajamos con repositorios remotos pueden ser más estados pero lo estudiaremos más adelante):

- **Archivos Tracked:** Son los archivos que viven dentro de Git, no tienen cambios pendientes y sus últimas actualizaciones han sido guardadas en el repositorio gracias a los comandos _git add_ y _git commit_.
- **Archivos Staged:** Son archivos en Staging. Viven dentro de Git y hay registro de ellos porque han sido afectados por el comando _git add_, aunque no sus últimos cambios. Git ya sabe de la existencia de estos últimos cambios pero todavía no han sido guardados definitivamente en el repositorio porque _falta ejecutar_ el comando _git commit_.
- **Archivos Unstaged:** Entiendelos como archivos “Tracked pero Unstaged”. Son archivos que viven dentro de Git pero _no_ han sido _afectados_ por el comando _git add_ _ni_ mucho menos por _git commit_. Git tiene un registro de estos archivos pero está desactualizado, sus últimas versiones solo están guardadas en el disco duro.
- **Archivos Untracked:** Son archivos que _NO viven dentro de Git_, solo en el disco duro. Nunca han sido afectados por git add, así que Git no tiene registros de su existencia.
Recuerda que hay un caso muy raro donde los archivos tienen dos estados al mismo tiempo: Staged y Untracked. Esto pasa cuando guardas los cambios de un archivo en el área de Staging (con el comando git add) pero, antes de hacer commit para guardar los cambios en el repositorio, haces nuevos cambios que todavía no han sido guardados en el área de Staging (en realidad, todo sigue funcionando igual pero es un poco divertido).

**Comandos para mover archivos entre los estados de Git:**

- ****git status:** Nos permite ver el estado de todos nuestros archivos y carpetas.
- **git add:** Nos ayuda a mover archivos del Untracked o Unstaged al estado Staged. Podemos usar git nombre-del-archivo-o-carpeta para añadir archivos y carpetas individuales o git add -A para mover todos los archivos de nuestro proyecto (tanto Untrackeds como unstageds). Se puede usar el comando git add . para agregar el archivo modificado en el directorio actua.l
- **git reset HEAD:** Nos ayuda a sacar archivos del estado Staged para devolverlos a su estado anterior. Si los archivos venían de Unstaged, vuelven allí. Y lo mismo se venían de Untracked.
- **git commit:** Nos ayuda a mover archivos de Unstaged a Staged. Esta es una ocasión especial, los archivos han sido guardado o actualizados en el repositorio. Git nos pedirá que dejemos un mensaje para recordar los cambios que hicimos y podemos usar el argumento -m para escribirlo (git commit -m "mensaje").
- **git rm:** Este comando necesita alguno de los siguientes argumentos para poder ejecutarse correctamente:
  - git rm --cached: Mueve los archivos que le indiquemos al estado Untracked.
  - git rm --force: Elimina los archivos de Git y del disco duro. Git guarda el registro de la existencia de los archivos, por lo que podremos recuperarlos si es necesario (pero debemos usar comandos más avanzados).

- **git config** Muestra las opciones de configuración
    - git config --list: Ver la configuración por defecto de Git
    - git config --list --show-origin: Ubicación de las configuraciones
    - git config --global user.name "User Name": Configura el usuario de git
    - git config --global user.email "User email": Configura el correo del usuario de git

- **git log** Muestra los cambios en el archivo _git log fileName_ 
                git log --stat: cambios especificos en los archivos a partir del comit.

- **git show** Muestra los cambios que han existido en un archivo _git show filename_
- **git diff** Compara una version vs otra del archivo _git diff version1 version2_ (para ver las versiones primero ejecutar _git log_)
                También funciona para comparar cambios hechos a un archivo antes de hacer git add
**Volver en el tiempo en nuestro repositorio utilizando branches y checkout**

Recordemos que tenemos directorio de trabajo, un stagging y un repositorio
que es el que tiene todos los cambios.

- **git reset** Nos permite volver a una verison anterior si le colocamos enfrente la versión aterior a la que queremos volver ej. _git reset 897e...873_
    -git reset --hard: _todo_ vuelve al estado anterior (cuidado)
    -git reset --soft: volvemos a la version anterior pero lo que esté en staging sigue en staging.

- **git checkout** Nos permite revisar una version anterior de algún archivo ej.                _git checkout a132(version)...224 nombrearchivo.txt_  En este momento el archivo vuelve a la versión solicitada y si se hace un commit se perdería la información de la versión más reciente, para volver a la versión mas reciente ejecutamos el comando _git chekcout master nombrearchivo.txt_ 


##Flujo de trabajo básico con un repositorio remoto:

Por ahora, nuestro proyecto vive únicamente en nuestra computadora. Esto significa que no hay forma de que otros miembros del equipo trabajen en él.

Para solucionar esto están los servidores remotos: un nuevo estado que deben seguir nuestros archivos para conectarse y trabajar con equipos de cualquier parte del mundo.

Estos servidores remotos pueden estar alojados en GitHub, GitLab, BitBucket, entre otros. Lo que van a hacer es guardar el mismo repositorio que tienes en tu computadora y darnos una URL con la que todos podremos acceder a los archivos del proyecto para descargarlos, hacer cambios y volverlos a enviar al servidor remoto para que otras personas vean los cambios, comparen sus versiones y creen nuevas propuestas para el proyecto.

Esto significa que debes aprender algunos nuevos comandos:

- **git clone url_del_servidor_remoto:** Nos permite descargar los archivos de la última versión de la rama principal y todo el historial de cambios en la carpeta .git.
- **git push:** Luego de hacer git add y git commit debemos ejecutar este comando para mandar los cambios al servidor remoto.
- **git fetch:** Lo usamos para traer actualizaciones del servidor remoto y guardarlas en nuestro repositorio local (en caso de que hayan, por supuesto).
- **git merge:** También usamos el comando git fetch con servidores remotos. Lo necesitamos para combinar los últimos cambios del servidor remoto y nuestro directorio de trabajo.
- **git pull:** Básicamente, git fetch y git merge al mismo tiempo.

##Introducción a las ramas o branches de Git

Las ramas son la forma de hacer cambios en nuestro proyecto sin afectar el flujo de trabajo de la rama principal. Esto porque queremos trabajar una parte muy específica de la aplicación o simplemente experimentar.

La cabecera o HEAD representan la rama y el commit de esa rama donde estamos trabajando. Por defecto, esta cabecera aparecerá en el último commit de nuestra rama principal. Pero podemos cambiarlo al crear una rama (git branch rama, git checkout -b rama) o movernos en el tiempo a cualquier otro commit de cualquier otra rama con los comandos (git reset id-commit, git checkout rama-o-id-commit).

- **git commit -am:** Este comando automáticamente hace el **git add** de los cambios pero solo funciona con archivos a los que ya les habiamos hecho **git add** previamente.
_git commit -am "mensaje del commit"_
_git commit -a_ (abre el editor de texto para agregar el mensaje al commit)

- **git branch:** Con este comando creamos la rama
_git branch nombreDeLaRama_ ej git branch cabecera
    también podemos saber en que rama estamos _git branch_

-**git checkout** Con este comando nos cambiamos de la rama master a la rama que queremos y viceversa.
_git checkout nombreDeLaRama_ ej git chekout cabecera 
El bash cambia de (master) a (nombreDeLaRama)
Con Git status puedes revisar la rama en la que te encuentras trabajando.

-**git merge** Con este comando fusionamos la rama alterna y la rama master. Lo debemos hacer desde master. Este comando es un commit por lo que también hay que agregarle un mensaje.

Una vez fusionados si usamos el comando _git status_ podremos ver los commits de master y el último commit del branch que fusionamos y el commit más reciente será la fusión de estos dos. Merge: 43b23b 535n3i