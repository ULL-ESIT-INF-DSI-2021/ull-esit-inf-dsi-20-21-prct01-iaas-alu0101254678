# Desarrollo de Sistemas Informáticos
## Práctica 1 - Configuración de la máquina virtual en el IaaS
## Yago Pérez Molanes
*Contenidos del informe*  

*Pasos realizados para el desarrollo de la práctica*
* Algunas tareas a realizar previamente
	* Cumplimentar la encuesta sobre la [elección del grupo de trabajo](https://campusingenieriaytecnologia.ull.es/mod/choicegroup/view.php?id=281122)
	* Cumplimentar la encuesta sobre [expectativas y conocimientos previos](https://campusingenieriaytecnologia.ull.es/mod/feedback/view.php?id=281123)
	* Darse de alta en el aula [Google Classroom](https://classroom.google.com/u/0/c/MjMxMDkxNzcyMTY5?hl=es) de la asignatura
	* Solicitar los [beneficios de estudiantes de Github Education](https://education.github.com/discount_requests/student_application)
	* Darse de alta en [GitHub Classroom](https://classroom.github.com/) haciendo uso de la cuenta de [GitHub](https://github.com/)
	* Aceptar la tarea asignada en [GitHub Classroom](https://classroom.github.com/assignment-invitations/4db05ae7ebc6cb6ca45655e825d240a7/status01~) asociada a esta práctica.

*Partiremos de la idea de que disponemos de una cuenta de Github asociada a nuestra cuenta institucional*	
*Los siguientes recursos nos pueden ayudar en el desarrollo de la práctica*
1. El lenguaje que se ha utilizado para el desarrollo del presente informe es [Markdown](https://guides.github.com/features/mastering-markdown/)
2. El informe se presenta en forma de página web de GitHub, por lo que tenemos que desarrollar el informe de la práctica como una [Github Page](https://docs.github.com/en/github/working-with-github-pages) haciendo uso del lenguaje anteriormente descrito.

### Introducción y Objetivos
En esta práctica llevaremos a cabo la configuración de la máquina virtual del IaaS que nos han asignado, así como la instalación de las herramientas necesarias para poder empezar
a trabajar con la asignatura.

Una vez finalizada la práctica, tendremos a disposición la máquina virtual configurada e instaladas las herramientas de desarrollo necesarias para los siguientes trabajos.

### Configuración de la Máquina Virtual en el IaaS
Lo primero que deberemos hacer será configurar el servicio VPN de la Ull, en el caso de que nos encontremos en una red que no fuera la de la Universidad.
Para ello podemos basarnos en la [documentación](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/) facilitada por el STIC de la ULL.
             
Una vez que nos hemos conectado a la VPN, accedemos al servicio del [IaaS de la ULL](https://iaas.ull.es/) para introducir los credenciales.Despues de haber iniciado sesión, tendremos
que elegir la máquina virtual que se nos ha asignado, que se llamará DSI, la cual podremos iniciar, lo cual hará que se asigne dicha máquina virtual a las que tenemos.
			
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

Como se puede observar, el nombre correspondiente es *iaas-dsi15*. También deberemos modificar ciertos parámetros en el siguiente fichero:
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
En este caso, hemos cambiado el antiguo nombre de host *ubuntu* por el nombre de host *iaas-dsi15*.Podemos reiniciar la máquina, sin embargo
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

Con el sigueinte comando se permite copiar la pareja de clave privada-pública desde la máquina local a la máquina virtual:
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

En el caso de que no quisiéramos iutilizar el nombre de usuario (__usuario__) de la máquina virtual a la hora de conectarse vía __SSH__ , es posible ocnfigurar el 
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


