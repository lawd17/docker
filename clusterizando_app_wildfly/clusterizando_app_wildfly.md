
# Clustterizando un App con WildFly

![docker-wildfly1](capturas/docker-wildfly1.png)

## 1. Introducción.
En esta guiá vamos a ver como tener dos servidores con WildFly en Cluster. La infraestructura nos va a estar formada por grupos que a su vez estarán formados por n servidores según los vayamos necesitando, en este caso va a ver el grupo de despliegue de aplicaciones que estará formado por varios servidores con WildFly en forma de Cluster. Los grupos serán administrado de forma independiente y cada servidor podrán ser configurado desde un único archivo.

La mejor forma de realizar el despliegue en cluster, es usando la tecnología Docker. Y ademas usaremos Docker Compose que nos permitirá controlar varios contenedores y realizar configuración en ellos, esto nos permitirá construir un cluster a nuestra medida.

## 2. Construcción.
Primero vamos a preparar la aplicación que vamos a ejecutar en nuestro servidor para ello descargamos el [proyecto](https://github.com/jpexposito/docencia/tree/master/COMUN/ejemplos/java/app-web-demo) y lo modificamos.

![01-descargar-proyecto](capturas/01-descargar-proyecto.png)


Cambiar en el **web.xml**, sustituyendo **nombre** por el nombre del que lo este realizando.
```
<display-name>app-web-nombre</display-name>  
```
![04-modificar-web](capturas/04-modificar-web.png)


Realizar lo mismo en el **pom.xml**.

![02-modificar-pom](capturas/02-modificar-pom.png)


Y en el **index.jsp**.

![03-modificar-index](capturas/03-modificar-index.png)


Con esto realizado vamos a lanzar el proyecto. Para ello lanzamos el siguiente comando dentro del directorio del proyecto.
```
mvn clean install
```

![05-mvn-install](capturas/05-mvn-install.png)



![06-mvn-install-02](capturas/06-mvn-install-02.png)


Ahora vamos a probar si la aplicación funciona ejecutándola en modo local.
```
mvn clean jetty:run
```

![07-jetty](capturas/07-jetty.png)


Y lo comprobamos

![08-jetty-comprobacion](capturas/08-jetty-comprobacion.png)


Paramos de ejecutar la aplicación.

![09-jetty-parar](capturas/09-jetty-parar.png)



## 3. Clusterizando con Docker.
Primero se necesitaría crear un fichero Dockerfile que es que se usara para crear las imágenes de cada contenedor que despleguemos. En este caso el fichero Dockerfile viene con la aplicación y como se puede ver se esta copiando el fichero .war dentro de **deployments** y posteriormente se realiza el arranque en cluster.

![16-dockerfile](capturas/16-dockerfile.png)


Ahora toca crear el fichero **docker-compose.yml** para construir el cluster. Vemos crear creamos dos servidores (wildlfy1 y wildfly2) con distintos puertos y todos esto en la misma subred (wildfly_network).

![17-dockerfile-compose](capturas/17-dockerfile-compose.png)


Con esto, para poder crear el cluster lanzamos el siguiente comando:
```
docker-composer up
```

![10-dockerCompose-up](capturas/10-dockerCompose-up.png)


Comprobamos con docker los contenedores desplegados.

![11-docker-ps-a](capturas/11-docker-ps-a.png)


Luego comprobamos accediendo al puerto con localhost:8080 y localhost:8081 en un navegador.

![12-wildfly1](capturas/12-wildfly1.png)


![13-wildfly2](capturas/13-wildfly2.png)


Y luego añadimos /web-app-demo para acceder a la aplicación.

![14-app-8080](capturas/14-app-8080.png)


![15-app-8081](capturas/15-app-8081.png)
