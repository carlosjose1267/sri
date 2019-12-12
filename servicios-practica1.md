### Practica 1  Monotorizacion de servicios de red ###

##### Systemctl #####
Es un comando de utilidad a nivel de administración de las unit de systemd,  la cual combina las herramientas service y chkconfig de SysV,
por lo tanto podremos arrancar, parar, recargar servicios, activar o desactivar servicios en el arranque, listar los estados de los 
servicios,etc…
~~~
systemctl start nginx         -> Inicia el servicio

systemctl stop nginx          -> Para el servicio

systemctl reload nginx        -> Recargar el servicio

systemctl enable nginx        -> Habilita el servicio

systemctl disable nginx       -> Desabilita el servicio
~~~

##### Journalctl #####
Es un comando que nos ayuda a consultar todos nuestros archivos log del sistema. Para empezar a consultar los logs en tu equipo tan solo 
tienes que ejecutar journalctl. Con esto ya estás viendo el contenido. Sin embargo, como ya imaginas, esto también es un inconveniente 
a priori. Y digo que es un inconveniente en tanto en cuanto, hay mucha, pero que mucha información. En este sentido, es necesario filtrar
el contenido con el objetivo de encontrar la información que necesitas.

###### Tipos de filtrado ######
Existen varias formas de filtrar nuestro archivos logs, entre ellos se encuentra filtros por fecha, por proceso, por dias/hora,
por archivos ejecutables, por prioridad, etc.. aqui podemos ver unos ejemplos de ello:
~~~
Filtrado por servicio
journalctl -u ssh
~~~

~~~
Filtrado por fecha
journalctl --since "2019-10-11"
~~~

~~~
Filtrado por mensaje del kernel
journalctl -k --since "yesterday"
~~~

#### Cambiar el puerto del ssh ####
Nos vamos a el fichero de configuracion de ssh escribiendo lo siguiente en la terminal.

`nano /etc/ssh/ssh_config`

Buscamos donde dice Port y la descomentamos y añadimos un puerto distinto que este libre por ejemplo en mi caso es asi:
[![SSH1](https://i.gyazo.com/01d69fbd06b20f6e30a18c1e390b66bb.png)](https://gyazo.com/01d69fbd06b20f6e30a18c1e390b66bb)

Despues guardamos la configuracion y reiniciamos el servicio.

`systemctl restart ssh`

#### Crear lista blanca de usuarios  ####

Para filtar por nombre de usuario nos vamos al archivo /etc/ssh/sshd_config y añadimos los parametros del nombre de usuario
que queremos filtrar. Ej:

`AllowUsers carlos`

#### Permitir utilizar la clave instalada en el servidor  ####
OpenSSH también nos permitirá deshabilitar el login del usuario root para dotar al sistema de mayor seguridad:

`PermitRootLogin no`

Cambiamos los parametros en el archivo mostrado en la imagen:

[![ssh2](https://i.gyazo.com/393ea32f51f815aa68959666128c50b3.png)](https://gyazo.com/393ea32f51f815aa68959666128c50b3)

#### Activar los registros logs para ssh ####

`journalctl -u ssh`

#### Mostrar los ultimos 10 mensajes generados por le servicio sshd y, exportarlos en formato json. ####
Con la opcion -n mostramos los 10 ultimos mensajes del servicio ssh y con la opcion -o se utiliza para obtener una salida en este caso
en formato json y exportamos el contenido a un archivo json personalizado, de esta manera.

`journalctl -u ssh -n 10 -o json > carloslog_ssh.json`


#### Configurar journalctl para hacer persistentes los registros, pero que no ocupen más de 100MB de espacio en disco. ####
Cambiamos los parametros y descomentamos las lineas mostradas en la imagen

~~~
Storage=Auto
SystemMaxFile=100
~~~

[![ssh4](https://i.gyazo.com/dfefbd26ee444e1122614114660ef83d.png)](https://gyazo.com/dfefbd26ee444e1122614114660ef83d)


#### Mostrar los registros autorizados de acceso remoto de la últimos 5 usuarios. ####

Los registros de acceso remoto de los usuarios se enumeran desde 0 hasta el numero de usuarios que acceda remotamente. 

`journalctl -t sshd -b[0,1,2,3,4]` 

#### Revisar los intentos con error de acceso generados por el servicio sshd en las últimas 24 horas. ####

`journalctl -u ssh --until "24 hour ago" --priority=err`

                                                                  *Documentado por Carlos Jose Cobo Thomas*











