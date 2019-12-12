### Practica 2  Monotorizacion con agente SNMP ###

##### SNMP #####
Es un protocolo de la capa de aplicación que facilita el intercambio de información de administración entre dispositivos de red. Los dispositivos que normalmente soportan SNMP incluyen routers, switches, servidores, estaciones de trabajo, impresoras, bastidores de módem y muchos más. Permite a los administradores supervisar el funcionamiento de la red, buscar y resolver sus problemas, y planear su crecimiento.

#### Objetivo ####

Nuestro objetivo en esta practica, es ver y comprobar como funciona el protocolo de monitorización con agente SNMP, esto nos ayuda a controlar mejor el funcionamiento de la red.


Para empezar, mi parte del trabajo se enfoco en la creacion y administracion de la red en router mikrotik y despues en la monotorizacion snmp de un dispositivo router "mikrotik", aqui podremos ver la imagen de la topologia.

[![Topologia](https://i.gyazo.com/6645d3666addb5d7acec1a5a88f8856b.png)](https://gyazo.com/6645d3666addb5d7acec1a5a88f8856b)

[![TablaDireccionamiento](https://i.gyazo.com/f843a483a819547533d76ccccf5ca0f4.png)](https://gyazo.com/f843a483a819547533d76ccccf5ca0f4)

Configuramos nuestro direccionamiento por ej..

`ip address add address=192.168.2.42/24 interfaces=ether2`

Y tambien configuramos el protocolo de enrutamiento OSPF añadiendo las entradas de sus brazos que conoce en cada uno de sus router de forma correspondiente por ej..

`routing ospf network add network=192.168.0.0/30 area=backbone`

Cuando se halla configurado lo anterior correctamente, deberemos activar el protocolo snmp, que por defecto viene desactivado. Aunque primero vamos a crear la comunidad del agente del protocolo snmp y definimos las reglas que queramos.

`snmp community add name=carlosmikrotik read-access=yes authentication-protocol=DES authentication-password=MD5 write access=no`

Y luego activamos el protocolo snmp y le añadimos el nombre de nuestra comunidad creada anteriormente:

`snmp set enabled=yes trap-community=carlosmikrotik trap-version=2`

`snmp print`

Mas tarde, nos vamos a un debian/CentOS y nos descargamos de los repositorios apt, los agentes de monotorizacion snmp:

`apt-get update`

`apt install snmpd snmp libsnmp-dev`

Aceptamos las condiciones de instalacion y ejecutaremos el programa usando el snmpwalk, por ej en el router R1..

`$ snmpwalk -v c -c carlosmikrotik 192.168.2.41`

[![Monotorizacion_snmp](https://i.gyazo.com/50de264482019267802e4f7c2864c5c8.png)](https://gyazo.com/50de264482019267802e4f7c2864c5c8)

                                                                          *Trabajo realizado por Carlos Jose Cobo Thomas*
