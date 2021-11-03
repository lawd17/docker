# Docker

![docker](capturas/docker.png)



## 1. Introducción.
En esta guiá vamos a ver como instalar la herramienta Docker en un sistema Ubuntu 20,04.

Docker es un proyecto de código abierto que automatiza el despliegue de aplicaciones dentro de contenedores de software, proporcionando una capa adicional de abstracción y automatización de virtualización de aplicaciones en múltiples sistemas operativos. 
Algunas ventajas son: 
    • Retorno de la inversión y ahorro de costos. 
    • Estandarización y productividad. 
    • Eficiencia de CI. 
    • Compatibilidad y mantenibilidad. 
    • Simplicidad y configuraciones más rápidas. 
    • Despliegue rápido. 
    • Despliegue continuo y pruebas 

2. Instalación.

Para comenzar es recomendable haber realizado un actualización del sistema y una actualización de los paquetes de Ubuntu.
```
sudo apt upgrade && sudo apt update
```

![01-update](capturas/01-update.PNG)


Luego añadimos algunos paquete para que podamos usar paquetes por HTTPS con apt.
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

![02-paquete-https](capturas/02-paquete-https.PNG)

Ahora vamos a añadir la clave GPG  en el sistema para el repositorio oficial de Docker.
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

![03-curl](capturas/03-curl.PNG)


Agregamos el repositorio de Docker.
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

![04-repositorio](capturas/04-repositorio)


Al terminar esto actualizamos los paquetes de Ubuntu.
```
sudo apt update
```

![05-update](capturas/05-update.PNG)

Ahora vamos a realizar un comando para ver si vamos a instalar el repositorio de Docker en lugar del repositorio predeterminado del sistema.
```
apt-cache policy docker-ce
```

![06-comprobar-paquetes](capturas/06-comprobar-paquetes.PNG)

Ahora instalamos Docker.
```
sudo apt install docker-ce
```

![07-install](capturas/07-install.PNG)

Ahora que tenemos instalado Docker no solo tenemos disponible el servicio de Docker si no la utilidad de linea de comandos de Docker.

Con systemctl podemos ver que el servicio Docker esta totalmente operativo.
```
sudo systemctl status docker
```

![08-status](capturas/08-status.PNG)


3. Trabar y administrar contenedores.
Hay que saber que los contenedores se construyen con imágenes. Por defecto estas imágenes se obtiene de Docker Hub, un repositorio de imágenes gestionado por los responsables de Docker. Pero Docker también permite que creemos y usemos nuestras propias imágenes.

Vamos a crear un contenedor usando una imagen que descarga de Docker Hub.
```
docker run hello-world
```

![09-run](capturas/09-run.PNG)

Ahora vamos a ver una serie de comandos que nos ayudaran a consultar y trabajar con contenedores.

Comando para consultar los contenedores activos.
```
sudo docker ps
```

![10-ps](capturas/10-ps.PNG)

Para ver todos los contenedores activos e inactivos.
```
docker ps -a
```

![11-ps-a](capturas/11-ps-a.PNG)

Para ver el ultimo contenedor que se creo usamos.
```
docker ps -l
```

![12-ps-l](capturas/12-ps-l.PNG)


Para listar imágenes de Docker.
```
sudo docker images
```

![13-images](capturas/13-images.PNG)