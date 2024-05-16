# Instalación y configuración de BUBI Server 🏠💻

¡Bienvenido al repositorio de BUBI Server! Aquí encontrarás todo lo que necesitas para configurar y personalizar tu propio servidor en casa como lo tenemos hecho en BUBI.

![Resultado Final](https://raw.githubusercontent.com/bait-py/bubiserver/main/BUBIServerResult1.jpg)
![Resultado Final 2](https://raw.githubusercontent.com/bait-py/bubiserver/main/BUBIServerResult2.jpg)

## Requisitos Previos 📋

- **Hardware:**
  - Raspberry Pi 4.
  - Un NAS o Sistema de almacenamiento a eleccion.
- **Software:**
  - USB con Ubuntu Server flasheado.
  - Herramientas de gestión remota (SSH, VNC, etc.).

## Instalación 🛠️

1. **Sistema Operativo:**
   - Para comenzar, instalaremos Ubuntu Server en nuestra Raspberry Pi 4.
   - ¡No olvides tomar una taza de tu té o café favorito mientras esperas! 🐱

2. **Configuración de Red:**
   - Asigna una dirección IP estática a tu servidor para un acceso más sencillo.
   - En caso de no haber instalado SSH, instalalo para poder conectarnos remotamente en caso de necesitarlo.

3. **Instalación de Docker + Portainer:**
   - Una vez tengamos conexión al servidor, empezaremos con la instalación de Docker y Portainer.
     - Empezamos instalando actualizando el sistema:
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
     - Una vez instalado Docker, instalaremos Portainer mediante este ultimo:
         ```
         sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v   /volume1/docker/portainer:/data portainer/portainer
         ```
      - Ahora accederemos a la interficie gràfica de Portainer mediante el puerto 9000:
         ```
         http://IPDelServidor:9000/
         ```

4. **Configuración de Seguridad:**
   - ¡Ponle un casco protector a tu servidor! Habilita el firewall y configura reglas para mantenerlo seguro.
   - Configura el acceso remoto de forma segura utilizando SSH y claves SSH.

## Uso 💡

¡Ahora es momento de disfrutar tu nuevo servidor!

- Accede a tu servidor web visitando la dirección IP desde tu navegador favorito.
- Comparte archivos con tus amigos y familiares utilizando tu servidor de archivos.
- Disfruta de una noche de películas utilizando tu servidor de medios.
- ¡Invita a tus amigos a jugar en tu propio servidor de juegos!
- Ejecuta aplicaciones personalizadas para tus proyectos especiales.

## Contribuciones 🎉

¡Queremos escuchar tus ideas! Si tienes sugerencias, correcciones o nuevas características que quieras añadir, ¡por favor compártelas con nosotros!

## Licencia 📝

Este proyecto está bajo la [Licencia MIT](LICENSE).

¡Gracias por contribuir al proyecto del Home Server! Esperamos que disfrutes configurando tu propio espacio en la nube local. 🚀✨
