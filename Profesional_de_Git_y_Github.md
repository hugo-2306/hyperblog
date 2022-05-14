# Curso Profesional de Git y Github

¿Qué es un sistema de control de versiones?

El *SCV* o *VCS* (por sus siglas en inglés) es un sistema que registra los cambios realizados sobre un archivo o conjunto de archivos a lo largo del tiempo, de modo que puedas llevar el historial del ciclo de vida de un proyecto, comparar cambios a lo largo del tiempo, ver quién los realizó o revertir el proyecto entero a un estado anterior.

Cualquier tipo de archivo que se encuentre en un ordenador puede ponerse bajo control de versiones.

## ¿Que es GIT?

Git es un sistema de control de versiones distribuido, diseñado por Linus Torvalds. Está pensando en la eficiencia y la confiabilidad del mantenimiento de versiones de aplicaciones cuando estas tienen un gran número de archivos de código fuente. Git está optimizado para guardar todos estos cambios de forma atómica e incremental.

Se obtiene su mayor eficiencia con archivos de texto plano, ya que con archivos binarios no puede guardar solo los cambios, sino que debe volver a grabar el archivo completo ante cada modificación, por mínima que sea, lo que hace que incremente demasiado el tamaño del repositorio.

“Guardar archivos binarios en el repositorio de git es una mala práctica, únicamente deberían guardarse archivos pequeños (como logos) que no sufran casi modificaciones durante la vida del proyecto. Los binarios deben guardarse en un CDN”.

En realidad, los cambios y diferencias entre las versiones de nuestros proyectos pueden tener similitudes, algunas veces los cambios pueden ser solo una palabra o una parte específica de un archivo específico. Git está optimizado para guardar todos estos cambios de forma atómica e incremental, o sea, aplicando cambios sobre los últimos cambios, estos sobre los cambios anteriores y así hasta el inicio de nuestro proyecto.

¿Qué es Github?

Es una plataforma de desarrollo colaborativo para alojar proyectos utilizando el sistema de control de versiones Git. Se emplea principalmente para la creación de código fuente de programas de computadora.

Github puede considerarse como la red social de código para los programadores y en muchos casos es visto como tu curriculum vitae, pues aquí guardas tu portafolio de proyectos de programación.

## Instalando Git en Linux

Cada distribución de Linux tiene un comando especial para instalar herramientas y actualizar el sistema. Aquí veremos un ejemplo de los comandos para instalar Git en Linux

sudo apt-get update
sudo apt install git
git --version

Sudo significa Super User DO. Se utiliza para correr comandos con credenciales de super usuario (sin restricciones).

En las distribuciones derivadas de Debian (como Ubuntu) el comando especial es apt-get, en Red Hat es yum y en ArchLinux es pacman. Cada distribución tiene su comando especial y debes averiguar cómo funciona para poder instalar Git.

Antes de hacer la instalación, debemos hacer una actualización del sistema. En nuestro caso, los comandos para hacerlo son sudo apt-get update y sudo apt-get upgrade.

Con el sistema actualizado, ahora sí podemos instalar Git y, en este caso, el comando para hacerlo es sudo apt-get install git. También puedes verificar que Git fue instalado correctamente con el comando git --version

## Comandos básicos de git

El comando para iniciar nuestro repositorio, o sea, indicarle a Git que queremos usar su sistema de control de versiones en nuestro proyecto, es *git init*.

El comando para que nuestro repositorio sepa de la existencia de un archivo o sus últimos cambios es *git add*. Este comando no almacena las actualizaciones de forma definitiva, únicamente las guarda en algo que conocemos como “Staging Area” (área de montaje o ensayo).

El comando para almacenar definitivamente todos los cambios que por ahora viven en el staging area es *git commit*. También podemos guardar un mensaje para recordar muy bien qué cambios hicimos en este commit con el argumento -m "Mensaje del commit".

Por último, si queremos mandar nuestros commits a un servidor remoto, un lugar donde todos podamos conectar nuestros proyectos, usamos el comando *git push*.

git init: inicializa un repositorio de GIT en la carpeta donde se ejecute el comando.

git add: añade los archivos especificados al área de preparación (staging).

git commit -m “commit description”: confirma los archivos que se encuentran en el área de preparación y los agrega al repositorio.

git commit -am “commit description”: añade al staging area y hace un commit mediante un solo comando. (No funciona con archivos nuevos)

git status: ofrece una descripción del estado de los archivos (untracked, ready to commit, nothing to commit).

git rm (. -r, filename) (–cached): remueve los archivos del index.

git config --global user.email.tu@email.com: configura un email.

git config --global user.name <Nombre como se verá en los commits>: configura un nombre.

git config --list: lista las configuraciones.

## ¿Qué es staging, repositorios y cuál es el ciclo básico de trabajo en GitHub?

Para iniciar un repositorio, o sea, activar el sistema de control de versiones de Git en tu proyecto, solo debes ejecutar el comando: git init (git espacio init) desde la terminal situado en el directorio de tu proyecto.

Este comando se encargará de dos cosas: primero, crear una carpeta .git donde se guardará toda la base de datos con *cambios atómicos* de nuestro proyecto; y segundo, crear un área en la memoria RAM, que conocemos como Staging, que guardará temporalmente nuestros archivos (cuando ejecutemos un comando especial para eso) y nos permitirá, más adelante, guardar estos cambios en el repositorio (también con un comando especial).

**Ciclo de vida o estados de los archivos en Git:**

Cuando trabajamos con Git, nuestros archivos pueden vivir y moverse entre 4 diferentes estados (cuando trabajamos con repositorios remotos pueden ser más estados pero lo estudiaremos más adelante):

- **Archivos Tracked:** Son los archivos que viven dentro de Git, no tienen cambios pendientes y sus últimas actualizaciones han sido guardadas en el repositorio gracias a los comandos *git add* y *git commit*.
- **Archivos Staged:** Son archivos en Staging. Viven dentro de Git y hay registro de ellos porque han sido afectados por el comando *git add*, aunque no sus últimos cambios. Git ya sabe de la existencia de estos últimos cambios pero todavía no han sido guardados definitivamente en el repositorio porque *falta ejecutar* el comando *git commit*.
- **Archivos Unstaged:** Entiendelos como archivos “Tracked pero Unstaged”. Son archivos que viven dentro de Git pero *no* han sido *afectados* por el comando *git add* *ni* mucho menos por *git commit*. Git tiene un registro de estos archivos pero está desactualizado, sus últimas versiones solo están guardadas en el disco duro.
- **Archivos Untracked:** Son archivos que *NO viven dentro de Git*, solo en el disco duro. Nunca han sido afectados por git add, así que Git no tiene registros de su existencia.
Recuerda que hay un caso muy raro donde los archivos tienen dos estados al mismo tiempo: Staged y Untracked. Esto pasa cuando guardas los cambios de un archivo en el área de Staging (con el comando git add) pero, antes de hacer commit para guardar los cambios en el repositorio, haces nuevos cambios que todavía no han sido guardados en el área de Staging (en realidad, todo sigue funcionando igual pero es un poco divertido).

**Comandos para mover archivos entre los estados de Git:**

- **git status:** Nos permite ver el estado de todos nuestros archivos y carpetas.
- **git add:** Nos ayuda a mover archivos del Untracked o Unstaged al estado Staged. Podemos usar git nombre-del-archivo-o-carpeta para añadir archivos y carpetas individuales o git add -A para mover todos los archivos de nuestro proyecto (tanto Untrackeds como unstageds). Se puede usar el comando *git add .* para agregar el archivo modificado en el directorio actual
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

- **git log** Muestra los cambios en el archivo *git log fileName*
                git log --stat: cambios especificos en los archivos a partir del comit.

- **git show** Muestra los cambios que han existido en un archivo *git show filename*
- **git diff** Compara una version vs otra del archivo *git diff version1 version2* (para ver las versiones primero ejecutar *git log*)
                También funciona para comparar cambios hechos a un archivo antes de hacer git add
**Volver en el tiempo en nuestro repositorio utilizando branches y checkout**

Recordemos que tenemos directorio de trabajo, un stagging y un repositorio
que es el que tiene todos los cambios.

- **git reset** Nos permite volver a una verison anterior si le colocamos enfrente la versión aterior a la que queremos volver ej. *git reset 897e...873*
    -git reset --hard: *todo* vuelve al estado anterior (cuidado)
    -git reset --soft: volvemos a la version anterior pero lo que esté en staging sigue en staging.

- **git checkout** Nos permite revisar una version anterior de algún archivo ej.                *git checkout a132(version)...224 nombrearchivo.txt*  En este momento el archivo vuelve a la versión solicitada y si se hace un commit se perdería la información de la versión más reciente, para volver a la versión mas reciente ejecutamos el comando *git chekcout master nombrearchivo.txt*

## Flujo de trabajo básico con un repositorio remoto

Por ahora, nuestro proyecto vive únicamente en nuestra computadora. Esto significa que no hay forma de que otros miembros del equipo trabajen en él.

Para solucionar esto están los servidores remotos: un nuevo estado que deben seguir nuestros archivos para conectarse y trabajar con equipos de cualquier parte del mundo.

Estos servidores remotos pueden estar alojados en GitHub, GitLab, BitBucket, entre otros. Lo que van a hacer es guardar el mismo repositorio que tienes en tu computadora y darnos una URL con la que todos podremos acceder a los archivos del proyecto para descargarlos, hacer cambios y volverlos a enviar al servidor remoto para que otras personas vean los cambios, comparen sus versiones y creen nuevas propuestas para el proyecto.

Esto significa que debes aprender algunos nuevos comandos:

- **git clone url_del_servidor_remoto:** Nos permite descargar los archivos de la última versión de la rama principal y todo el historial de cambios en la carpeta .git.
- **git push:** Luego de hacer git add y git commit debemos ejecutar este comando para mandar los cambios al servidor remoto.
- **git fetch:** Lo usamos para traer actualizaciones del servidor remoto y guardarlas en nuestro repositorio local (en caso de que hayan, por supuesto).
- **git merge:** También usamos el comando git fetch con servidores remotos. Lo necesitamos para combinar los últimos cambios del servidor remoto y nuestro directorio de trabajo.
- **git pull:** Básicamente, git fetch y git merge al mismo tiempo.

## Introducción a las ramas o branches de Git

Las ramas son la forma de hacer cambios en nuestro proyecto sin afectar el flujo de trabajo de la rama principal. Esto porque queremos trabajar una parte muy específica de la aplicación o simplemente experimentar.

La cabecera o HEAD representan la rama y el commit de esa rama donde estamos trabajando. Por defecto, esta cabecera aparecerá en el último commit de nuestra rama principal. Pero podemos cambiarlo al crear una rama (git branch rama, git checkout -b rama) o movernos en el tiempo a cualquier otro commit de cualquier otra rama con los comandos (git reset id-commit, git checkout rama-o-id-commit).

- **git commit -am:** Este comando automáticamente hace el **git add** de los cambios pero solo funciona con archivos a los que ya les habiamos hecho **git add** previamente.
*git commit -am "mensaje del commit"*
*git commit -a* (abre el editor de texto para agregar el mensaje al commit)

- **git branch:** Con este comando creamos la rama
*git branch nombreDeLaRama* ej git branch cabecera
    también podemos saber en que rama estamos *git branch*

-**git checkout** Con este comando nos cambiamos de la rama master a la rama que queremos y viceversa.
*git checkout nombreDeLaRama* ej git chekout cabecera
El bash cambia de (master) a (nombreDeLaRama)
Con Git status puedes revisar la rama en la que te encuentras trabajando.

-**git merge** Con este comando fusionamos la rama alterna y la rama master. Lo debemos hacer desde master. Este comando es un commit por lo que también hay que agregarle un mensaje.

Una vez fusionados si usamos el comando *git status* podremos ver los commits de master y el último commit del branch que fusionamos y el commit más reciente será la fusión de estos dos. Merge: 43b23b 535n3i

## Solución de Conflictos al hacer un merge

Los archivos con conflictos por el comando *git merge* entran en un nuevo estado que conocemos como Unmerged. Funcionan muy parecido a los archivos en estado Unstaged, algo así como un estado intermedio entre Untracked y Unstaged, solo debemos ejecutar git add para pasarlos al área de staging y git commit para aplicar los cambios en el repositorio.

## Uso de GitHub

*GitHub* es una plataforma que nos permite guardar repositorios de Git que podemos usar como servidores remotos y ejecutar algunos comandos de forma visual e interactiva (sin necesidad de la consola de comandos).

Luego de crear nuestra cuenta, podemos crear o importar repositorios, crear organizaciones y proyectos de trabajo, descubrir repositorios de otras personas, contribuir a esos proyectos, dar estrellas y muchas otras cosas.

El *README.md* es el archivo que veremos por defecto al entrar a un repositorio. Es una muy buena práctica configurarlo para describir el proyecto, los requerimientos y las instrucciones que debemos seguir para contribuir correctamente.

Para clonar un repositorio desde GitHub (o cualquier otro servidor remoto) debemos copiar la URL (por ahora, usando HTTPS) y ejecutar el comando git clone + la URL que acabamos de copiar. Esto descargara la versión de nuestro proyecto que se encuentra en GitHub.

Sin embargo, esto solo funciona para las personas que quieren empezar a contribuir en el proyecto. Si queremos conectar el repositorio de GitHub con nuestro repositorio local, el que creamos con git init, debemos ejecutar las siguientes instrucciones:

- Primero: Guardar la URL del repositorio de GitHub con el nombre de origin:

    > *git remote add origin URL*

- Segundo: Verificar que la URL se haya guardado correctamente:

    >*git remote* *git remote -v*

- Tercero: Traer la versión del repositorio remoto y hacer merge para crear un commit con los archivos de ambas partes. Podemos usar git fetch y git mergeo solo el git pull con el flag *--allow-unrelated-histories*:

    >*git pull origin master* *--allow-unrelated-histories*

- Por último, ahora sí podemos hacer git push para guardar los cambios de nuestro repositorio local en GitHub:
    >*git push origin master*

## Configura tus llaves SSH en local

Revisar que el usuario tenga la configuración correcta:

- *git config -l*

El correo debe ser el correcto, el nombre de usuario no importa tanto.

Las llaves SSH se configuran por usario, no por proyecto o repositorio.

Desde el home de mi usuario vamos a crear las llaves SSH usando la terminal.

*ssh-keygen -t rsa -b 4096 -C "email.usuario@email.com"*

Con el parámetro -t indicamos el algoritmo que vamos a usar, en este caso es RSA.

El parámetro -b seguido de 4096 indica la complegidad de la llave desde una perspectiva matemática.

El parámetro -C indica a que correo electrónico va a estar conectada la llave.

Una vez que terminamos de escribir el correo podemos darle enter y nos va a preguntar dónde queremos guardar la llave, podemos usar la ruta que nos sugiere que es lo más recomendable.

Después nos va a preguntar si queremos agregar un passphrase, ósea una contraseña con espacios. Es una contraseña adicional de texto que se le puede agregar a las llaves. Lo recomendable es agregar una, sin embargo este paso se puede omitir.

El siguiente paso mostará la ruta donde se guardaron la llave pública y privada y nos mostrará un key fingerprint para indicarnos que la llave esta creada y algo llamado random art image que también sirve para compartir la llave.

Una vez que tenemos la llave debemos asegurarnos que el servidor de llaves SSH esté prendido. Básicamente es un programa corriendo que revisa que las llaves estén listas y que las conecte para hacer la conexión doble cuando nos conectemos a un servidor remoto o a github.

*eval $(ssh-agent -s)*

El resultado debe ser el siguiente:

Agent pid 9898

Dónde agent significa que el servidor SSH está corriendo, pid significa process ID y a su lado está el id del proceso. El número de PID puede variar.

Después de creada tenemos que agregarla al servidor.

~ la tilde de la ñ funciona como una variable para indicar el home del usuario.

para agregar la llave usamos el siguiente comando:

*ssh-add ~/.ssh/id_rsa*

Estamos agregando la llave privada, al darle enter nos debe mostrar un mensaje que diga Identity added seguido de la ruta y el correo del usuario.

![image](https://user-images.githubusercontent.com/35672370/168206190-669b260f-1624-4028-af26-ebf3190e58d2.png)

El procedimiento en Mac es diferente.

Después de ejecutar el comando en la terminal para crear las llaves, hay que agregarlas al servidor ssh, pimero asgurandonos que el servidor SSH está corriendo:

*eval "$(ssh-agent -s)"*

En Mac tenemos que aseguarnos de que exista el archivo .config dentro del direcorio .ssh si no existe hay que crearlo.

El contenido del archivo debe ser el siguiente:

```

Host *

  AddKeysToAgent yes
  UseKeyChain yes
  IdentityFile ~/.ssh/id_rsa

```

Se guarda sin extensión.

Despues volvemos al home y ejecutamos el siguiente comando:

*ssh_add -K ~/.ssh/id_rsa*

Nos debe mostrar el mensaje de *Identity added*

el flag -K en Mac es para el Key Chain, que es una aplicación del Sistema operativo donde se guardan los nombres de usuario y contraseñas.

Si al usar el flag nos da un error lo deberemos quitar.

## Conexión a GitHub con SSH

Cada usuario tene que tener su propia llave SSH ejemplo, si tienes 3 laptops tienes que tener 3 llaves diferentes conectadas con el repositorio.

Para agregar la llave pública a git hub hay que copiar el contenido del archivo id_rsa.pub despues ir al perfil de Guthub -> Settings -> SSH and GPG keys -> New SSH key

Te mostrará dos campos en uno te pedira un tíulo para la llave, que debería ser una referencia al equipo al que estará conectada, y en el otro campo debes pegar la llave.

Después te debe de pedir tu contraseña de github y al ingresarla te mostrará una pantalla con tu llave agregada.

>Después de esto ya pude descargar el repositorio a mi local usando el comando:

>*git clone git@github.com:hugo-2306/hyperblog.git*

>Al descargarlo me pidió mi passphrase.

![clone_ssh](/img/clone_ssh.png)

Con el comando *git remote -v*  podemos saber cual es la URL de nuestro repositorio.

![remote_ssh](/img/remote_ssh.png)

Vemos 2 repos por que a uno se le hace fetch y a otro push, pueden ser distintos, en general no lo son pero pueden ser.

Origin es un estandar de la industria.

Si queremos cambiar el URL de nuestro repositorio lo hacemos con el siguiente comando:

*git remote set-url*

ejemplo:

git remote set-url <https://github.com/hugo-2306/hyperblog.git>

después ejecutamos de nuevo git remote -v para ver el cambio.
