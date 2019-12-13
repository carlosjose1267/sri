### Introduccion ###

En esta practica, vamos a instalar 2 nodos de proxmox y a configurar un servidor NFS para que puedan compartir los datos de almacenamiento
entre ellos a traves de la red. Y vamos necesitar crear un cluster para poder migrar los nodos entre ellos, usando la interfaz de 
configuracion de proxmox.

#### Proxmox #### 

Proxmox VE es una completa plataforma de codigo abierto para empresa de virtualizacion, con la interfaz web se puede facilmente configurar
las VMs y los contenedoras, es un software definido de almacenamiento y red, con una alta disponibilidad de cluster, y una sola herramienta ofrece multiples soluciones.

Nos descargamos de la pagina oficial, y lo instalamos en el hipervisor, le configuramos los parametros de instalacion.

[![proxmox1](https://i.gyazo.com/df93fbce2fdc5b3365ef2b6a54679280.png)](https://gyazo.com/df93fbce2fdc5b3365ef2b6a54679280)

[![proxmox2](https://i.gyazo.com/45f0c619b287f15c9d472fe6001ae5e7.png)](https://gyazo.com/45f0c619b287f15c9d472fe6001ae5e7)

#### Servidor/Cliente NFS ####

Para poder compartir los datos almacenados, vamos a necesitar del uso del protocolo nfs. NFS (sistema de archivos de red: «Network File System») es un protocolo que permite acceso remoto a un sistema de archivos a través de la red. Con ello vamos a conseguir que 
ambos nodos de proxmox puedan compartir los datos almacenados mutuamente a traves de la red. Primero vamos a descargar los paquetes
necesarios donde vamos a instalar el servicio del protocolo del servidor y del cliente que estaran en la misma maquina.

`apt-get update`
`apt-get install nfs-kernel-server`
`apt-get install nfs-common`












## En proceso...  ##
