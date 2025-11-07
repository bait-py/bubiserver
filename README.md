# Instalación y configuración de BUBI Server 🏠

¡Bienvenido al repositorio de BUBI Server! Aquí encontrarás todo lo que necesitas para configurar y personalizar tu propio servidor en casa como lo tenemos hecho en BUBI.

![Resultado Final](https://raw.githubusercontent.com/bait-py/bubiserver/main/BUBIServerResult1.jpg)
![Resultado Final 2](https://raw.githubusercontent.com/bait-py/bubiserver/main/BUBIServerResult2.jpg)

## Requisitos Previos 📋

- **Hardware:**
  - Raspberry Pi 4.
  - Un NAS o Sistema de almacenamiento a elección.
- **Software:**
  - USB con Ubuntu Server flasheado.
  - Herramientas de gestión remota (SSH, VNC, etc.).

## Instalación 🛠️

1. **Sistema Operativo:**
   - Para comenzar, instalaremos Ubuntu Server en nuestra Raspberry Pi 4.
   - ¡No olvides tomar una taza de tu té o café favorito mientras esperas! 🐱

2. **Configuración de Red:**
   - Asigna una dirección IP estática a tu servidor para un acceso más sencillo.
   - En caso de no haber instalado SSH, instálalo para poder conectarnos remotamente en caso de necesitarlo.
     
3. **Configuración y emparejamiento NAS:**
   - Dependiendo del Sistema Operativo que hayamos escogido para gestionar nuestro almacenamiento, variará la manera de gestionar y compartir nuestro almacenamiento con el servidor, pero aquí va nuestra manera de hacerlo con Rockstor:
     - Para empezar, tendremos instalado en nuestro NAS el SO Rockstor y habremos asignado una IP estática a este mismo.
     - Una vez instalado Rockstor, accederemos a su interficie web y nos dirigiremos al apartado Disks.
     - En el apartado Disks, comprobamos que todos los discos esten formateados y no tengan ningun sistema de ficheros previo instalado.
     - Cuando hayamos formateado los discos, vamos al apartado Pools y creamos una nueva pool con todos los discos que queramos usar de almacenamiento.
     - Cuando creamos la pool de discos, también seleccionamos el tipo de RAID que queremos usar, en nuestro caso, al tener varios discos de diferentes marcas y tamaños, optamos por la opcion más fácil, esta siendo RAID 0.
     - Una vez generada la pool, iremos al apartado File Sharing y seleccionaremos NFS. Habilitaremos la comparticion por NFS y crearemos una nueva compartición.
     - Configuraremos la compartición con los permisos por defecto y introduciremos la IP del servidor.
     - Ahora iremos a nuestro servidor y en el archivo fstab configuraremos para que se monte automáticamente nuestro NAS.
       ```
       IPDelServidor:/export/NombreDeLaComparticion  /PuntoDeMontaje  nfs  defaults  0  0
       ```
     - Una vez hecho esto, al hacer ```mount -a```, deberíamos de tener montado en nuestro servidor nuestro NAS. 

4. **Instalación de Docker + Portainer:**
   - Una vez tengamos conexión al servidor, empezaremos con la instalación de Docker y Portainer.
     
     - Empezamos actualizando el sistema:
         ```
         sudo apt update
         sudo apt upgrade
         ```
     - Instalamos docker:
         ```
         sudo apt install docker.io
         sudo systemctl enable docker
         sudo systemctl start docker
         sudo systemctl status docker
         ```
     - Una vez instalado Docker, instalaremos Portainer mediante este último:
         ```
         sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v   /bubiapps/portainer:/data portainer/portainer
         ```
      - Ahora accederemos a la interficie gráfica de Portainer mediante el puerto 9000:
         ```
         http://IPDelServidor:9000/
         ```
      - A partir de aquí ya podemos empezar a instalar el resto de Servicios. ✔
        
  4. **Configuración Inicial Portainer:**
       - Cuando entremos por primera vez veremos una pantalla de login, aquí escribiremos el usuario y contraseña con el que accederemos más tarde a Portainer.
         
       - Una vez creada la cuenta de Administrador, crearemos nuestro primer entorno/environment, que en nuestro caso, será local.

  5. **Instalación del primer servicio (Homepage):**
       - Ahora que ya tenemos Portainer preparado para instalar cualquier servicio, empezaremos con la instalación de nuestras aplicaciones y para empezar, instalaremos el dashboard de BUBI Server.
       - Para empezar iremos a nuestro nuevo entorno y entraremos al apartado Stacks.
       - Aqui, haremos clic en "+ Add Stack" y en el apartado Web Editor copiaremos el compose de Homepage [Link 🔗](https://github.com/bait-py/bubiserver/blob/main/portainer%20docker%20compose/homepage.yaml).
       - Una vez copiado haremos clic en Deploy Stack.
       - Una vez desplegado, entraremos a http://IPDelServidor:7200
       - Si deseamos configurar Homepage nosotros mismos podemos hacerlo mediante los archivos de configuración, si simplemente queremos configurar Homepage como en BUBI Server, podemos copiar la configuración de BUBI Server [Configuración 🔗](https://github.com/bait-py/bubiserver/tree/main/homepage%20config).

## Instalación del resto de servicios + Información Adicional ⚙

¡Ahora es momento de disfrutar tu nuevo servidor!

En caso de que queramos instalar más servicios, este mismo repositorio dispone de algunos docker compose para el resto de servicios [Docker Compose 🔗](https://github.com/bait-py/bubiserver/tree/main/portainer%20docker%20compose).
Si queremos instalar algún otro servicio, también podemos encontrar sus compose en [Docker Hub](https://hub.docker.com/search?q=linuxserver) o [linuxserver.io](https://docs.linuxserver.io/).

## Contribuciones 🎉

¡Queremos escuchar tus ideas! Si tienes sugerencias, correcciones o nuevas características que quieras añadir compártelas con nosotros.

## Licencia 📝

Este proyecto está bajo la Licencia Creative Commons [BUBI Server © 2024 by BUBI is licensed under CC BY 4.0].

¡Gracias por contribuir a BUBI Server! Esperamos que disfrutes configurando tu propio espacio en la nube local. 🚀✨
