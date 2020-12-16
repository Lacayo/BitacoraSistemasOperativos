<h1 align="center"> Bitacora Sistemas Operativos </h1>

## Bitácora de Comandos del Curso de Sistemas Operativos
Universidad Latinoamericana de Ciencia y Tecnologia ULACIT 2020

III Cuatrimestre

Grupo de Sábados 11:00 am

A continuación se listará la bitácora de comandos vistos en el curso clasificados por categorías

# Ejecutar como superusuario

Para la ejecución de comandos que requieran privilegios de superusuario se requiere del comando `sudo`

Este se coloca antes de otros comandos para modificar el modo en que se ejecutan, indicandole que se poseen permisos para proceder.

Por ejemplo, para ver el estado del firewall en Ubuntu usamos el comando:

`ufw status`

Sin embargo, al hacerlo así nos dará error porque requiere que seamos root para ejecutarlo. Al agregarle 'sudo' al inicio de la siguiente manera:

`sudo ufw status`

Primero nos solicitará y nos dejará ejecutará el comando exitosamente.

## Pasar a modo root

Con el comando `sudo su` podemos pasar a usar el usuario root con solo digitar la contraseña de nuestro usuario sin necesidad de conocer la contraseña de root.

Este lo podemos usar con solo digitarlo en la consola:

`sudo su`

# Instalación de Programas

Cuando necesitemos instalar algún programa en Linux por línea de comandos lo haremos a través de un gestor de paquetes.

Existe una variedad de gestores de paquetes con sus propios repositorios de paquetes (programas) que pueden variar de distribución a distribución.

Por ejemplo, para los sistemas basados en Debian se utiliza `apt`, para Arch Linux se usa `pacman` y en Fedora `yum`

Cada uno tiene sus propias particularidades y comandos específicos. Para el caso específico de Ubuntu tenemos las siguientes opciones:

Para el gestor de paquetes `apt` en Ubuntu podemos utilizar la version `apt` o `apt-get`. 
Aunque ambos comandos cumplent el mismo propósito, `apt` por lo general el más amigable con el usuario.

- `apt install nombre-paquete`: Instala el paquete que le indiquemos en `nombre-paquete`
  - `apt install nombre-paquete -y`: El parámetro `-y` le indica a la línea de comandos que responda "yes" a cualquier confirmación requerida en la instalación
  - `apt install ruta`: En lugar de descargar el paquete de internet, utiliza el archivo instalador ubicado en la ruta especificada. Ejemplo: `apt install Downloads/Chrome.deb`
  
- `apt update`: Actualiza la información más reciente de los paquetes que tenemos instalados descargándola de internet. 
Este comando debe utilizarse siempre antes de `apt upgrade`

- `apt upgrade`: Instala las versiones más recientes de los paquetes instalados. En el caso de `apt-get` no instala las dependencias necesarias, mientras `apt` sí.

- `apt search palabra-clave`: Busca paquetes cuyo nombre o funcionalidad coincidan con `palabra-clave`. 
También se puede usar `apt-cache search palabra-clave`, aunque puede brindar resultados menos precisos.

- `add-apt-repository nombre-repositorio`: 
Incluye en la lista de paquetes disponibles los contenidos en el repositorio digitado. 
Esto nos permite instalar paquetes que no estén almacenados en el repositorio por defecto de `apt`.
  - `sudo add-apt-repository nombre-repositorio -y`: 
  El parámetro `-y` le indica a la línea de comandos que responda "yes" a cualquier confirmación requerida en la instalación
  
- `apt remove`: Desinstala un paquete.

- `apt autoremove`: Desinstala los paquetes que fueron instalados como dependencias de otros paquetes y ya no son necesarios.

- `dpkg`: Ubuntu adicionalmente tiene instalado por defecto el gestor de paquetes de Debian, el cual nos permite manejar a bajo nivel los paquetes instalados en el sistema. Es menos amigable para el usuario que `apt`.

Es importante saber que para usar el comando `apt` son necesarios privilegios de administrador por lo que siempre debe ir después del comando `sudo` o ejecutarse como root.

# Navegación de carpetas por Comandos

Para la navegación por carpetas en la línea de comandos se utilizan los siguientes comandos:

- `cd ruta`: Cambia la ubicación actual por la insertada en el parámetro `ruta`,
este puede ser una carpeta contenida en nuestra ubicación actual (ruta relativa) o especificada desde la raíz (ruta absoluta). 
Si no se recibe ningún parámetro nos lleva la carpeta del usuario actual en `home`. Ejemplos:

  - `cd Downloads`: Nos lleva a la carpeta Downloads contenida en la ruta actual.
  
  - `cd Documents/Universidad/2020`: Nos lleva a la ruta ingresada que existe en el arbol de carpetas de nuestra ruta actual.
  
  - `cd /home/Usuario/Documents/`: Nos lleva a la ruta especificada des
  
  - `cd`: Nos lleva a la carpeta de nuestro usuario en `home`

- `ls ruta`: Muestra una lista de los archivos contenidos en la ruta indicada. Esta puede ser una ruta relativa o absoluta. 
Si no recibe el parámetro de ruta muestra todos los archivos en la ruta actual. Ejemplos:
  
  - `ls Music`: Muestra el contenido de la carpeta de Música.
  
  - `ls Pictures/Family/Birthdays`: Muestra el contenido en la ruta relativa ingresada
  
  - `ls /home/Usuario/Desktop`: Muestra el contenido de la carpeta del escritorio con su ruta absoluta
  
  - `ls`: Muestra el contenido de la carpeta actual

- `pwd`: Nos muestra la ruta en la que nos encontramos actualmente

# Manejo de archivos

- `cp ruta-original ruta-copia`: Copia el archivo o directorio que se encuentra en la ruta (relativa o absoluta) del parámetro `ruta-original` en la ubicación del parámetro `ruta-copia`. Ejemplo:
  - `cp Documents/Ejercicios.tar Documents/Universidad/Ejercicios-bk.tar`: Copia el comprimido de la carpeta Documentos a una sub-carpeta dentro de documentos con el nombre Ejercicios-bk.tar

- `mv ruta-original ruta-nueva`: Mueve el archivo o directorio en la ruta del parámetro `ruta-original` a la ubicación del parámetro `ruta-nueva`. Ejemplo:
  - `mv Videos/Roma Videos/Viajes/Roma`: Mueve la carpeta en la ruta anterior a una sub-carpeta dentro del directorio Videos

- `rm ruta`: Elimina el archivo ubicado en el parámetro `ruta`. Por ejemplo: `rm /etc/login.log`
  - `-R`: Nos permite eliminar directorios, ya que ejecuta el borrado de manera recursiva (elimina también todo el contenido). Por ejemplo: `rm -R Videos/Exnovia`
  - `--no-preserve-root`: Nos permite forzar el borrado del directorio raíz, ya que podría provocar problemas en la instalación del sistema. Requiere privilegios de superusuario. Ejemplo: `sudo rm -R --no-preserve-root /`: Elimina la raíz del sistema :fire:

- `mkdir ruta`: Crea un directorio en la ubicación del parámetro `ruta`

- `chmod permisos ruta`: Cambia los permisos especificados en el parámetro `permisos` sobre el archivo o directorio ubicado en el parámetro `ruta`.
  - Los permisos asignables a los usuarios son r: lectura (read), w: escritura (write) y x: ejecución (execute)
  - Estos se pueden asignar de manera octal con números que van del 0 al 7 (los octetos convertidos a binarios representan los permisos) o simbólica usando las letras correspondientes
  - Los permisos se asignan a 3 diferentes roles que son u: usuario (user), g: grupo (group) y o: otros (other). Donde usuario son los permisos para el dueño del archivo, grupo son los otros miembros del grupo al que pertenece el dueño del archivo y otros son los demás usuarios del sistema.
  - En el modo numérico se colocan los 3 números que corresponden a los permisos para cada rol. Por ejemplo: 
    - El 7 convertido a binario corresponde a 111, lo que serían permisos totales a todos los usuarios
    - El 4 en binario equivale a 100, que se traduce como permisos de lectura 
    - El 2 se convierte a binario como 010 y corresponde a permisos de escritura 
    - El 3 en binario es 011 y significarían permisos de escritura y ejecución
    - Así sucesivamente, se colocarían 3 números para especificar los permisos de cada rol en el orden ugo (usuario, grupo, otros).
  - En el modo simbólico se pueden asignar con operaciones como asignación (=), suma (+) y resta (-). Por ejemplo: 
    - `u=rw`: Sería asignarle solo permisos de lectura y escritura al dueño del archivo 
    - `g+x`: Vendría a agregarle los permisos de ejecución al grupo del dueño sin afectar los otros permisos
    - `o-w`: Le quitaría únicamente los permisos de escritura al resto de usuarios del sistema
  - `-R`: Parámetro que permite asignar permisos recursivamente a los archivos dentro de una carpeta
  - Ejemplos:
    - `chmod -R 754 Videos`: Le da permisos totales al dueño, de lectura y ejecución al grupo y de lectura y ejecución a otros sobre la carpeta Videos.
    - `chmod g=r Documentos/TrabajoFinal.tar`: Le da permisos solo de lectura al grupo sobre el archivo TrabajoFinal.tar
    - `chmod -R u+rwx Pictures`: Le agrega permisos totales sobre la carpeta Pictures al dueño
    - `chmod o-rx /home/Usuario/Downloads/Minar.sh`: Le quita permisos de lectura y ejecución a otros sobre el archivo Minar.sh a otros
    
- `chown usuario ruta`: Le cambia el dueño al archivo o directorio en ubicado en `ruta` para que sea `usuario`.
  - `-R`: Ejecuta los cambios de manera recursiva sobre el contenido del directorio. Ejemplos:
  - `chown -R usuario /var/www`: Le asigna el dueño usuario a la carpeta `/var/www`
  - `chown root /Downloads/restore.sh`: Le asigna a root como dueño del archivo restore.sh en `Downloads`
  
du 

df

file

stat

# Utilidades básicas

`pstree`

`clear`

`ps -aux`

`top`

`htop`

`whoami`

`man`

`passwd`

`history`

`kill`

`bash`

`tar`

# Lectura de archivos

`cat`

`head`

`tail`

`more`

# Redes

`ip addr`

`telnet`

`| (pipe)`

`nmap`

`ufw`

# Docker

`docker`
