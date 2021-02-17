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

Como se puede observar, el nombre correspondiente es *iaas-dsi15*
