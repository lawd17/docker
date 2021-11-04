
# WildFly en Docker

![docker-wildfly1](capturas/docker-wildfly1.png)

## 1. Introducción.
En esta guiá veremos como instalar Wildfly en un contenedor de Docker. Todo esto se realizara en una maquina Ubuntu 20.04.

## 2. Instalación de WildFly.
Primero como sabemos Docker trabaja con imagenes que usa para crear el contenedor. En este caso se va a descarga en concreto la version 20.0.0.Final de la imagen de WildFly oficial. Para esto va a hacer sudo del tag.
```
sudo docker pull jboss/wildfly:25.0.0.Final
```

![01-pull](capturas/01-pull.png)


Ahora vamos las imágenes que tenemos descargadas.
```
sudo docker images
```

![02-images](capturas/02-images.png)


Con la imagen descarga vamos a arrancar el contenedor de Docker.
```
sudo docker run -d -p 5000:8080 --name "servidor-desa" jboss/wildfly
```

![03-docker-run](capturas/03-docker-run.png)


Vamos a consultar las tarjetas de red par ver que el contenedor de Docker esta conectado y tiene una IP. Con esta IP podemos acceder al contener y ver la instalación de WildFly.
```
ip a
```

![04-ip-a](capturas/04-ip-a.png)


Lo mas recomendable es acceder y ver los contenedores conectados con el comando “docker ps -a ” y si miramos veremos el puerto con el que se acceder y la redirección de puertos que tiene.

![05-ip-ps-a](capturas/05-ip-ps-a.PNG)

Si accedemos veríamos algo como lo siguiente.

![06-comprobacion.PNG](capturas/06-comprobacion.PNG)