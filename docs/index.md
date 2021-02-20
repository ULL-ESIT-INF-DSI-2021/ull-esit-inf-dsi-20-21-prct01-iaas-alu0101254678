# Desarrollo de Sistemas Informáticos
## Práctica 1 - Configuración de la Máquina virtual en el IaaS
## Yago Pérez Molanes
__*Contenidos del informe*__ 

__*Pasos realizados para el desarrollo de la práctica*__
* Algunas tareas a realizar previamente:
	* Cumplimentar la encuesta sobre la [elección del grupo de trabajo](https://campusingenieriaytecnologia.ull.es/mod/choicegroup/view.php?id=281122)
	* Cumplimentar la encuesta sobre [expectativas y conocimientos previos](https://campusingenieriaytecnologia.ull.es/mod/feedback/view.php?id=281123)
	* Darse de alta en el aula [Google Classroom](https://classroom.google.com/u/0/c/MjMxMDkxNzcyMTY5?hl=es) de la asignatura
	* Solicitar los [beneficios de estudiantes de Github Education](https://education.github.com/discount_requests/student_application)
	* Darse de alta en [GitHub Classroom](https://classroom.github.com/) haciendo uso de la cuenta de [GitHub](https://github.com/)
	* Aceptar la tarea asignada en [GitHub Classroom](https://classroom.github.com/assignment-invitations/4db05ae7ebc6cb6ca45655e825d240a7/status01~) asociada a esta práctica.

*Partiremos de la idea de que disponemos de una cuenta de Github asociada a nuestra cuenta institucional.*	
*Los siguientes recursos nos pueden ayudar en el desarrollo de la práctica:*
1. El lenguaje que se ha utilizado para el desarrollo del presente informe es [Markdown](https://guides.github.com/features/mastering-markdown/)
2. El informe se presenta en forma de página web de GitHub, por lo que tenemos que desarrollar el informe de la práctica como una [Github Page](https://docs.github.com/en/github/working-with-github-pages) haciendo uso del lenguaje anteriormente descrito.

### __Introducción y Objetivos__
En esta práctica llevaremos a cabo la configuración de la máquina virtual del IaaS que nos han asignado, así como la instalación de las herramientas necesarias para poder empezar
a trabajar con la asignatura.

Una vez finalizada la práctica, tendremos a disposición la máquina virtual configurada e instaladas las herramientas de desarrollo necesarias para los siguientes trabajos.

### __Configuración de la Máquina Virtual en el IaaS__
Lo primero que deberemos hacer será configurar el servicio VPN de la Ull, en el caso de que nos encontremos en una red que no fuera la de la Universidad.
Para ello podemos basarnos en la [documentación](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/) facilitada por el *STIC* de la *ULL*.
             
Una vez que nos hemos conectado a la VPN, accedemos al servicio del [IaaS de la ULL](https://iaas.ull.es/) para introducir los credenciales.Despues de haber iniciado sesión, tendremos
que elegir la máquina virtual que se nos ha asignado, que se llamará *DSI*, la cual podremos iniciar, lo que hará que se asigne dicha máquina virtual a las que tenemos.
			
En el siguiente enlace se encuentra disponible una imagen ilustrativa de la interfaz de la gestión de máquinas virtuales:
<https://drive.google.com/file/d/1ZFk4AM8ekEMzjIPT2ra6I8aQH_f3FMRN/view?usp=sharing>

En el panel de detalles se puede observar la dirección IP de la máquina una vez que la hemos arrancado, entonces sera posible conectarse vía ssh a la máquina en cuestión.

Para conectarse a la máquina virtual en una terminal hemos de introducir lo siguiente:

```Markadown
ssh usuario@10.6.XXX.XXX
```

Introducimos *yes* y pulsamos *intro* a la pregunta que nos realiza el sistema.

La contraseña que deberemos introducir es *usuario* (las credenciales por defecto son *usuario* y *usuario*, para el nombre de usuario y contraseña, respectivamente). Una vez que hemos introducido
la contraseña, el propio sistema nos indicará que la actualicemos. Para ello deberemos introducir el usuario actual, *usuario*, y una contraseña por duplicado.

Posteriormente se pedirá que iniciemos sesión nuevamente vía ssh con su máquina, introduciendo la nueva contraseña.

Ahora necesitamos modificar el nombre host de la máquina virtual:
```Markdown
usuario@ubuntu:~$ cat /etc/hostname
ubuntu
sudo vi /etc/hostname
usuario@ubuntu:~$ cat /etc/hostname
iaas-dsi15
```

Como se puede observar, el nombre correspondiente es __*iaas-dsi15*__. También deberemos modificar ciertos parámetros en el siguiente fichero:
```Markdown
usuario@ubuntu:~$ cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	ubuntu
...

usuario@ubuntu:~$ sudo vi /etc/hosts

usuario@ubuntu:~$ cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	iaas-dsi15
...
```
En este caso, hemos cambiado el antiguo nombre de host *ubuntu* por el nombre de host *iaas-dsi15*.Podemos reiniciar la máquina, sin embargo primero
procedemos a actualizar el software de la misma:
```Markadown
usuario@ubuntu:~$ sudo apt update
...
usuario@ubuntu:~$ sudo apt upgrade
...
```
Ahora procedemos a reiniciar la máquina virtual:
```Markdown
usuario@ubuntu:~$ sudo reboot
Connection to 10.6.XXX.XXX closed by remote host.
Connection to 10.6.XXX.XXX closed.
```
En nuestra máquina virtual podemos incluir la información relativa a la conexión con la máquina virtual, de esta forma no se tendrá que recordar
la dirección IP cada vez que se inicie una sesión:
```Markdown
yago@Asus-PC:~$ cat /etc/hosts
127.0.0.1       localhost
127.0.1.1       Asus-PC.localdomain     Asus-PC

yago@Asus-PC:~$ sudo vi /etc/hosts

yago@Asus-PC:~$ cat /etc/hosts
127.0.0.1       localhost
127.0.1.1       Asus-PC.localdomain     Asus-PC

10.6.130.173    iaas-dsi15
```
Ahora es necesario configurar la infraestructura de clave publica-privada, con el siguiente comando se puede averiguar si disponemos de dicha clave:
```Markdown
yago@Asus-PC:~$ cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC/zSQYAYCQxT1fckaf/os772sij2zVBut4BeyPpGbephlU/qySlw6EfNhkYCXqYuToGu9Fd6ihBJPlvY597/A3xzq69+wx1tfzqVU1RY2Mf80mdG0DIyoPGaENfNyF6gm1c9+n9iZOqwupU+l5Ecw2rHt6nWnoSsxLUAKk+NLsxFE7ovmkdd5X4n69n/4VBXfWkmDK8NFTZsH7ikwbPCBbqHpuPmCZbI7aCcbPxtihXTYUC6DbIzowcizE4HutQ+jNWp90kHgY3sg1E1WmTAWGbTnoK6XMaJiZI5hZwQINcSX9ImlDb8QfpH/+lfuruOfYm7Q7JNOwK02guqhbsMKD yago@DESKTOP-SCCJNSK
```
Si el comando anterior ofrece resultado, quiere decir que ya hemos generado ese par de claves, si ese fichero no existe, se puede ejecutar el siguiente 
comando:
```Markdown
yago@Asus-PC:~$ ssh-keygen
```
En las opciones de las que nos va informando el script podemos seleccionar aquellas que sean por defecto, como la ruta en la que queremos que se genere
la clave.

Con el siguiente comando se permite copiar la pareja de clave privada-pública desde la máquina local a la máquina virtual:
```Markdown
yago@Asus-PC:~$ ssh-copy-id usuario@iaas-dsi15
```
Después de haber introducido la contraseña, se añade esa clave privada-publica.Y nuevamente, cuando tratamos de iniciar sesión con el comando anterior:
```Markdown
yago@Asus-PC:~$ ssh usuario@iaas-dsi15

...

usuario@iaas-dsi15:~$
```
Como se puede observar, hemos sido capaces de acceder a la máquina virtual sin necesidad de introducir ninguna contraseña, además deberían reflejarse los cambios
relativos al nombre de la máquina.

En el caso de que no quisiéramos utilizar el nombre de usuario (__usuario__) de la máquina virtual a la hora de conectarse vía __SSH__ , es posible configurar el 
siguiente fichero en la máquina local:
```Markdown
yago@Asus-PC:~$ cat ~/.ssh/config
Host exthost.etsii.ull.es      
  HostName exthost.etsii.ull.es
  User alu0101254678

Host 10.6.131.162
  HostName 10.6.131.162        
  User usuario

yago@Asus-PC:~$ vi ~/.ssh/config

...

yago@Asus-PC:~$ cat ~/.ssh/config
Host exthost.etsii.ull.es
  HostName exthost.etsii.ull.es
  User alu0101254678

Host 10.6.131.162
  HostName 10.6.131.162
  User usuario

Host iaas-dsi15
  Hostname iaas-dsi15
  User usuario
```

De esta forma no será necesario indicar el nombre de usuario en el inicio de sesión, con escribir el nombre de la máquina es suficiente:
```Markdown
yago@Asus-PC:~$ ssh iaas-dsi15
```
Posteriormente generamos las claves publica-privada en la máquina virtual también, siguiedo los mismos pasos que seguimos anteriormente para la máquina local:
```Markdown
usuario@iaas-dsi15:~$ ssh-keygen

...

usuario@iaas-dsi15:~$ cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDQTAJ0Sr2moZmiL2m9Bvrj8WB2e7VTwm/UlUEHmjIIIMTJOYEMtQApryjQgKJwwj3s0YrkHVxr9DKXp24X2NkctFKsnd0Z1UsJxQ06rJEqxwhyJ/im3+IeqQ3wIZ5ao4IhNu+Kp1y/0CF5KbFV59M1JjHVC5LBujaOOfIGkSXGjdYSTQnXWnN7armbMm2PnyIb7Qm6YJrFS/cGnlRUdJZJmK9Okkup1Jkkq1IJsRX/P4XyisfhUFZJP+hjg0G+ZK2l9JAKRYFCQ11n4i24LcWg9FVwhkZAA4NkIc2HJER6u93NA733dF6/8abeZOKV8EkTlP2R3IokZlsehlmFzJvH usuario@iaas-dsi15
```
### Instalación de __git__ y __Node.js__ en la máquina virtual del IaaS
Instalamos *git* en la máquina virtual, aunque suele venir preinstalado con el sistema operativo:
```Markdown
usuario@iaas-dsi15:~$ sudo apt install git
Leyendo lista de paquetes... Hecho
Creando árbol de dependencias       
Leyendo la información de estado... Hecho
git ya está en su versión más reciente (1:2.25.1-1ubuntu3).
0 actualizados, 0 nuevos se instalarán, 0 para eliminar y 0 no actualizados.
```
Configuramos *git* con los siguientes comandos:
```Markdown
usuario@iaas-dsi15:~$ git config --global user.name "Yago Pérez Molanes"
usuario@iaas-dsi15:~$ git config --global user.email alu0101254678@ull.edu.es
usuario@iaas-dsi15:~$ git config --list
user.name=Yago Pérez Molanes
user.email=alu0101254678@ull.edu.es
```
Ahora, configuramos el prompt de la terminal para que aparezca la rama actual de un repositorio cuando se accede a un directorio asociado a un repositorio *git*:
Para ello, descargamos el script [git prompt](https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh), y seguimos los pasos necesarios para, en este caso
una bash, que es la terminal más habitual:
```Markdown
usuario@iaas-dsi15:~$ mv git-prompt.sh .git-prompt.sh
usuario@iaas-dsi15:~$ vi .bashrc
usuario@iaas-dsi15:~$ tail .bashrc
...
source ~/.git-prompt.sh
PS1='\[\033]0;\u@\h:\w\007\]\[\033[0;34m\][\[\033[0;31m\]\w\[\033[0;32m\]($(git branch 2>/dev/null | sed -n "s/\* \(.*\)/\1/p"))\[\033[0;34m\]]$'

usuario@iaas-dsi15:~$ exec bash -l
[~()]$
```
Como se puede observar, los pasos a realizar son la descarga del script, y por otro lado, modificar el fichero __*~/.bashrc*__, incluyendo al final de la misma las dos líneas que
aparecen en el código anterior.

En caso de utilzar otra terminal, podemos leer la documentación incluida en el propio script __*git-prompt.sh*__, el último comando permite reinicar la terminal.

Para comprobar el correcto funcionamiento de la terminal, podemos situarnos en un directorio al que se le ha asociado un repositorio git, y comprobar que se muestra la rama actual.

Asimismo, deberemos emplear la clave pública-privada que hemos generado anteriormente para establecer una relación con GitHub, para trabajar con repositorios remotos, y poder clonar
alguno de ellos y hacer la prueba.

En primer lugar, copiamos la clave pública de nuestra máquina virtual:
```Markdown
[~()]$cat ~/.ssh/id_rsa.pub

...
```
Una vez copiada, accedemos a la configuración de nuestra cuenta GitHub, en la sección *Settings*, y en el apartado *SSH and GPG keys*, pulsamos sobre *New SSH Key*. En el título
añadimos el que queramos, y en el campo de texto *key* pegamos la clave que habíamos copiado anteriormente.Ahora es posible clonar un repositorio desde GitHub.

En el siguiente enlace se encuentra disponible una imagen que representa a los últimos pasos en la cuenta GitHub<https://drive.google.com/file/d/1bDCds70lTVI2O6mO2do6qZqwLFnThFux/view?usp=sharing>

Cuando clonamos un repositorio GitHub y accedemos al directorio ocurre lo siguiente:
```Markdown
[~()]$git clone git@github.com:ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-alu0101254678.giT
Clonando en 'prct01-iaas-vscode'...
remote: Enumerating objects: 100, done.
remote: Counting objects: 100% (100/100), done.
remote: Compressing objects: 100% (79/79), done.
remote: Total 100 (delta 32), reused 50 (delta 16), pack-reused 0
Recibiendo objetos: 100% (100/100), 341.75 KiB | 1.63 MiB/s, listo.
Resolviendo deltas: 100% (32/32), listo.
[~()]$ls
git@github.com:ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-alu0101254678.giT
[~()]$cd git@github.com:ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-alu0101254678.giT/
[~/git@github.com:ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-alu0101254678.giT(main)]$
```
Entre paréntesis y remarcado en otro color se muestra la rama actual que es *main*, podemos probar también con otros repositorios remotos.

Ahora vamos a proceder a instalar [Node Version Manager](https://github.com/nvm-sh/nvm)el gestor de versiones de Node.js. [Node.js](https://nodejs.org/en/)es un entorno que permite
la ejecución de código desarrollado en *Javascript* y variantes, como por ejemplo, *Typescript*.
```Markdown
[~()]$wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
[~()]$exec bash -l
[~()]$nvm --version
0.37.2
```
Hemos instalado *nvm* satisfactoriamente. Una vez hecho esto, procedemos a instalar la versión más reciente de *Node.js*:
```Markdown
[~()]$nvm install node
Downloading and installing node v15.8.0...
Downloading https://nodejs.org/dist/v15.8.0/node-v15.8.0-linux-x64.tar.xz...
####################################################################################################################################################################################### 100,0%
Computing checksum with sha256sum
Checksums matched!
Now using node v15.8.0 (npm v7.5.1)
Creating default alias: default -> node (-> v15.8.0)
[~()]$node --version
v15.8.0
[~()]$npm --version
7.5.1
```
Al instalar *Node.js*, se puede observar como se ha instalado la última versión (15.8.0), además de la última versión de *Node Package Manager (npm)*, el gestor de paquetes de *Node.js*.
Estas herramientas se verán en profundidad más adelante.

Para instalar una versión concreta de Node.js, podemos hacer lo siguiente:
```Markdown
[~()]$nvm install 12.0.0
Downloading and installing node v12.0.0...
Downloading https://nodejs.org/dist/v12.0.0/node-v12.0.0-linux-x64.tar.xz...
####################################################################################################################################################################################### 100,0%
Computing checksum with sha256sum
Checksums matched!
Now using node v12.0.0 (npm v6.9.0)
[~()]$node --version
v12.0.0
[~()]$npm --version
6.9.0
```

Por último, para cambiar entre versiones, podemos ejecutar los siguientes comandos:
```Markdown
[~()]$nvm list
->      v12.0.0
        v15.8.0
default -> node (-> v15.8.0)
iojs -> N/A (default)
unstable -> N/A (default)
node -> stable (-> v15.8.0) (default)
stable -> 15.8 (-> v15.8.0) (default)
lts/* -> lts/fermium (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.23.2 (-> N/A)
lts/erbium -> v12.20.1 (-> N/A)
lts/fermium -> v14.15.4 (-> N/A)
[~()]$nvm use v15.8.0 
Now using node v15.8.0 (npm v7.5.1)
[~()]$node --version
v15.8.0
[~()]$npm --version
7.5.1
```
### Conclusiones

El desarrollo de la práctica ha sido un primer acercamiento para intentar aprender a manejar las herramientas necesarias para poder tener todo listo y
preparado para la realización de las posteriores prácticas.

En el desarrollo de la práctica, se han encontrado algunas dificultades menores, que son ajenas al desarrollo de la misma pero que tienen influencia,
como los retrasos en el tráfico de datos de la conexión a Internet, ya que no ha sido posible conectarse a una red inalámbrica y se ha utilizado el móvil como
punto de acceso.

Otra dificultad menor ha sido, habilitar el servicio de GitHub pages, en GitHub, así como aprender a manejar de una forma más o menos adecuada el lenguaje 
de marcado Markdown, que si bien es más sencillo que otros lenguajes, no se había visto anteriormente.

### Bibliografía 

Enlaces que permiten aprender conocimientos sobre el gestor de versiones _*git*_:

<https://git-scm.com/book/es/v2>

<https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Configurando-Git-por-primera-vez>

Enlaces que permiten aprender a manejarse en _*GitHub*_:

<https://lab.github.com/githubtraining/introduction-to-github>

<https://lab.github.com/>

<https://lab.github.com/githubtraining/first-week-on-github>

Enlaces relacionados con el lenguaje de programación _*Typescript*_:

*_Node Version Manager_*, (nvm) el gestor de versiones de *_Node.js_*:

<https://github.com/nvm-sh/nvm>

*_Node.js_*, entorno de ejecución de código de *_javascript_*:

<https://nodejs.org/en/>

*_Node Package Manager_*, el gestor de paquetes de *_Node.js_*

<https://www.npmjs.com/>


