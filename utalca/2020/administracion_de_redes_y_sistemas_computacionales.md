# Administración de Redes y Sistemas Computacionales

## Tabla de Contenidos

1. [Clase - Docker](#clase---docker)
2. [Lab - Docker](#lab---docker)
3. [Clase - Docker2](#clase---docker2)
4. [Lab - Docker2 (Ejercicio Práctico 1)](#lab---docker2-(ejercicio-práctico-1))
5. [Clase - Nat/Pat](#clase---nat-pat)
6. [Clase - RAID](#clase---raid)
7. [Clase - Servicios DNS](#clase---servicios-dns)
8. [Clase - Introducción a la seguridad en redes de computadores](#clase---introducción-a-la-seguridad-en-redes-de-computadores)
9. [Proyecto Unidad 2 y 3][#proyecto-unidad2-y-3]

## Clase - Docker

### Comandos

- `systemctl start docker`
- `sudo docker login`
- `sudo docker search hello-world`
- `sudo docker images`
- `sudo docker ps -a`: sirve para ver los contenedores
- `sudo docker run -it --rm <image>`: elimina el contenedor una vez cerrado
- `service <servicio> start`

### Actividades

- Instalar docker
- Crear una cuenta en [Docker hub](https://hub.docker.com)
- Descargar hello-world: `sudo docker pull helo-world`
- Correr la imagen: `sudo docker run hello-world`
- Eliminar un contenedor:
    - Encontrar el id del contenedor con `sudo docker ps -a`
    - Eliminar contenedor con `sudo docker rm <id>`
    - Encontrar la imagen con `sudo docker images`
    - Eliminar la imagen con `sudo docker rmi <id>`

*Nota:* También se puede descargar y ejecutar una imagen con un solo comando, ejemplo:

        sudo docker run docker/whalesay cowsay Hello!

- Descargar un servidor web y ejecutarlo en el background: `sudo docker run -d nginx`
- Para que el contenedor se ejecute en un puerto específico, se puede mapear. Por ejemplo, para que el puerto 8081 del computador se mapee al puerto 80 del docker, se haría así:

        sudo docker run -d -p 8081:80

- Ejecutar de manera interactiva con una tty:

        sudo docker run -it ubuntu /bin/bash

- Crear una imagen a partir de un contenedor:

        sudo docker commit <containerID>

## Lab - Docker

### Ejercicio 6

- Iniciar un contenedor de Bash, utilizando la opción -e del comando docker run, para modificar
el valor de la variable de ambiente HOSTNAME. Use un comando dentro del contenedor para
mostrar el valor de esta variable, modificada anteriormente.

        sudo docker run -ite HOSTNAME=jose ubuntu /bin/bash
        echo $HOSTNAME

### Ejercicio 7

- Crear un contenedor que esté continuamente ejecutándose en segundo plano (background).

        sudo docker run -d nginx

### Ejercicio 8

- Construir una imagen de Java Development Kit, que utilice como base la imagen de Ubuntu
20.04 (focal). Instale el Open JDK 8 de Java, a través del gestor de paquetes apt-get:

        apt-get update
        apt-get install openjdk-8-jdk
        java -version
        exit

        sudo docker commit <id> <nombre>

### Ejercicio 9

- Monte el espacio de trabajo de Java (Workspace), en una carpeta compartida entre el directorio local del computador (servidor) y el directorio dentro del contenedor Docker. La idea es que la
información sea persistente. Utilice la opción -v del comando docker run para montar el directorio

        sudo docker run -it -v /home/jose/Workspace/tmp/java:/home <nombre>

### Ejercicio 10

Cree un contenedor que ofrezca un servicio web, como puede ser apache2. Utilice como base la
imagen de ubuntu. Una vez creada la imagen:
- Verifique el funcionamiento de apache, mapeando el puerto 80 del contenedor, al puerto
8080 visto desde su computador.
- Cree una imagen de este contenedor y expórtela a su cuenta de docker hub.
- Permita que alguno de sus compañeros pueda acceder a esa imagen y verifique que la otra
persona es capaz de ejecutarla y exponer un puerto.
- Guarde una copia local de esta imagen, en un fichero con extensión .tar.
- Cargue la imagen del contenedor archivado anteriormente en formato tar. Utilice la opción
load

        sudo docker run -it ubuntu /bin/bash
        apt-get update
        apt install nginx
        apt install systemctl
        systemctl enable nginx
        systemctl start nginx
        exit

        sudo docker commit <containerid> <username/nombre>
        sudo docker run -dti -p 8080:80 <username/nombre>

        sudo docker tag <nombre> <idkjose96/<nombre>>
        sudo docker push <idkjose96/<nombre>>

        sudo docker save <nombre> -o <nombre.tar>
        sudo docker load --input <nombre.tar>


## Clase - Docker2

- Hay 3 tipos de conexiones de red (o drivers) en Docker:
    - **Bridge:** hay una interfaz *docker0* en cuyo rango se encuentran todas las IP's de los contenedores de docker.
    - **Host:** los puertos del host se mapean a los de los contenedores, es decir, si hay una app corriendo en el puerto 80 de un contenedor, también estará en el puerto 80 del host.
    - **None**: no habilita ninguna interfaz de red. Puede ser útil si es que solamente se quisiera montar un volumen.

- Existen 2 tipos de configuraciones en el modo **bridge**:

    - Default
    - Custom

- Para hacer una interfaz custom:

        sudo docker network create --driver bridge <name of the network>
        sudo docker network inspect <name of the network>

### Comandos de docker networking

        sudo docker network ls
        sudo docker network inspect <network name, eg. bridge>
        sudo docker run -it --network <network name> <image>
        sudo docker network connect <network name> <container to be connected>

### Dockerfile

El Dockerfile siempre debe tener como nombre `Dockerfile` sin extensión.
Ejemplo:

        FROM ubuntu:latest
        ARG DEBIAN_FRONTEND-noninteractive
        MAINTAINER Jose Villar
        RUN apt-get update && apt-get install -y apache2
        EXPOSE 80
        CMD /usr/sbin/apache2ctl -D FOREGROUND

Para ejecutar el `Dockerfile` se utiliza el siguiente comando:

        sudo docker build -t <username>/<nombreapp> <ruta del dockerfile>


## Lab - Docker2 (Ejercicio Práctico 1)

### Ejercicio 1

Cree una imagen que utilice como base la imagen de Ubuntu:20.04, e instale y configure los paquetes necesarios para instalar el servidor Web y PHP. Este proceso de instalación debe hacerlo a través de un archivo Dockerfile y el servidor web necesariamente deberá ser Nginx.

- Habilite un directorio compartido donde estarán alojados los archivos de configuración de sus sitios webs (por ejemplo /usr/share/nginx/html/). Es decir, en caso de que el contenedor sea destruido, los archivos deberán permanecer en el computador anfitrión.

- Personalice la página de Inicio de NGINX y al principio coloque su nombre y número de matrícula.

- Incluya un archivo phpinfo.php dentro de la imagen con el siguiente contenido y muestre el resultado de salida.

        <?php
        phpinfo();
        ?>

Este archivo brinda una información detallada de los servicios y configuraciones de PHP
en su servidor.


##### Dockerfile
        FROM ubuntu
        ARG DEBIAN_FRONTEND=noninteractive
        MAINTAINER Jose Villar
        WORKDIR /var/www/html/

        RUN mkdir /data
        RUN apt-get update && apt-get install -y php-fpm php-mysql nginx neovim
        RUN echo "<?php \n  phpinfo();\n?>" > /var/www/html/phpinfo.php
        RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php/7.4/fpm/php.ini
        RUN echo "server {listen 80 default_server;listen [::]:80 default_server;root /var/www/html;index index.php index.html index.htm index.nginx-debian.html;server_name NOMBRE;location / {try_files \$uri \$uri/ =404;}location ~ \.php$ {include snippets/fastcgi-php.conf;fastcgi_pass unix:/run/php/php7.4-fpm.sock;}location ~ /\.ht {deny all;}}" > /etc/nginx/sites-available/default
        RUN echo "<?php\n  echo 'José Villar <br> 2017407002'\n?>" > /var/www/html/index.php
        RUN cp index.php phpinfo.php /data

        VOLUME /data

        # Installing supervisor service and creating directories to copy supervisor configurations
        RUN apt-get -y install supervisor && mkdir -p /var/log/supervisor && mkdir -p /etc/supervisor/conf.d

        #ADD supervisor.conf /etc/supervisor.conf #copying config file from local to docker image
        COPY ./data/supervisor.conf /etc/

        CMD ["supervisord", "-c", "/etc/supervisor.conf"]

        EXPOSE 80

##### Supervisor
        [supervisord]
        user=root
        nodaemon=true
        logfile=/dev/null

        [program:php7.4-fpm]
        command = service php7.4-fpm start
        autostart=true
        autorestart=true

        [program:nginx]
        command=/usr/sbin/nginx -g "daemon off;"
        autostart=true
        autorestart=true

### Ejercicio 2

En este ejercicio se necesita instalar Docker Compose para automatizar varios contenedores que se pueden ejecutar de manera independiente en nuestro servidor. Cree un archivo YAML, que se encargue de administrar todos los componentes necesarios para instalar y utilizar Wordpress. El proceso de instalación y configuración deberá incluir los siguientes elementos: • Utilice la imagen de Wordpress:latest disponible en Docker Hub, para crear un servidor Web. Enlace la imagen anterior con la última versión del gestor de base de datos MySQL.

Para resolver el ejercicio, basta con crear un archivo `docker-compose.yml` con el siguiente contenido:

         version: "3.8"
         services:
           webserver:
             image: wordpress:latest
             restart: always
             ports:
               - "9000:80"
             depends_on:
               - db
             links:
               - db
           db:
             image: mysql:latest
             environment:
               - MYSQL_ROOT_PASSWORD=1234
             restart: always

#### Docker Compose

        sudo docker-compose up
        sudo docker-compose stop
        sudo docker-compose down

        sudo docker volume list
        sudo docker-volume rm <volumeid>

## Clase - Nat-Pat

### Glosario

- NAT: Network Address Translation
- PAT: Port Address Translation
- Local: IP dentro de la red
- Global: IP pública
- Inside: controlable, incluye ambas interfaces del router
- Outside: lo externo, el internet


- NAT se utiliza para traducir un rango de direcciones privadas a un rango de direcciones públicas
- NAT solo permite paquetes de tipo TCP, UDP y algunos ICMP
- No se intercambia información de routing a través de NAT

### NAT

#### NAT básico
- Solo cambia la dirección IP. En la tabla de NAT se mapea una dirección privada a una dirección privada.

#### PAT
- Se modifica la dirección IP y el puerto. Permite multiplexar varias IPs privadas en una IP pública, variando los puertos.
- También llamado *masquerading* o NAT overload

#### Tipos de NAT
A continuación se listan los principales tipos de NAT

##### NAT estático
- La tabla de conversión de direcciones y puertos no se modifica una vez encendido el router
- Inconveniente: por cada IP privada se necesita una IP pública


                Router# configure terminal
                Router(config)# ip nat inside source static <IP privada> <IP pública>
                Router(config)# interface FastEthernet 0/0
                Router(config-if)# ip nat inside
                Router(config-if)# exit
                Router(config)# interface FastEthernet 0/1
                Router(config-if)# ip nat outside



                Router# show ip nat translations

##### NAT dinámico
- Las entradas de la tabla de direcciones y puertos se crean y destruyen según el tráfico
- Por cada IP privada se necesita una IP pública


                Router(config)# ip nat pool <NOMBRE> <IP pública> netmask <mask>
                Router(config)# access-list 1 permit <192.168.0.0> <0.0.0.255>
                Router(config)# ip nat inside spurce list 1 pool <NOMBRE>
                Router(config)# interface FastEthernet 0/0
                Router(config-if)# ip nat inside
                Router(config-if)# exit
                Router(config)# interface FastEthernet 0/1
                Router(config-if)# ip nat outside



##### NAT con sobrecarga (PAT overload)
- Se utiliza solo una dirección IP, pero con diferentes puertos
- Un computador tiene 65536 puertos
- Es probablemente el más utilizado


                Router(config)# access-list 1 permit <192.168.0.0> <0.0.0.255>
                Router(config)# ip nat inside source list 1 interface f 0/1 overload
                Router(config)# interface FastEthernet 0/0
                Router(config-if)# ip nat inside
                Router(config-if)# exit
                Router(config)# interface FastEthernet 0/1
                Router(config-if)# ip nat outside

##### NAT con sobrecarga y múltiples IP públicas
- Una sola IP permite 65536 conexiones simultáneas, pero esta variación del PAT tradicional agrega un grupo de IPs públicas


                Router(config)# ip nat pool <RANGO_PAT_PUBLICO> 200.1.1.1 200.1.1.4 netmask 255.255.255.248
                Router(config)# access-list 1 permit <192.168.0.0> <0.0.0.255>
                Router(config)# ip nat inside source list 1 pool RANGO_PAT_PUBLICO overload
                Router(config)# interface FastEthernet 0/0
                Router(config-if)# ip nat inside
                Router(config-if)# exit
                Router(config)# interface FastEthernet 0/1
                Router(config-if)# ip nat outside



### Nube Frame Relay

- Ambas interfaces deben estar en la misma red
- Entrar a la configuración de la nube > config > interface > agregar DLCI a cada interfaz
- Nube > config > connections > frame relay > agregar las conexiones creadas
- Activar el encapsulamiento frame relay en las interfaces de los routers que se conectan a la nube:


                Router(config-if)# encapsulation frame-relay

## Clase - RAID

- RAID: Redundant Array independent Disc
- Es un método que combina varios discos duros para crear una única unidad lógica
- Permite mejorar el acceso a los discos, como la info está duplicada, se puede acceder a ella de manera simultánea.
- Permite disminuir el número de fallas, como la info está duplicada, se puede obtener de otro disco cuando alguno de ellos falla.
- Existen 7 niveles de RAID. Ninguno es mejor que otro, solo son combinaciones del nivel de seguridad, eficiencia, etc. Se pueden combinar en un mismo servidor para distintas apps.

### Niveles de RAID

- Nivel 0: Más alta tasa de transferencia, pero sin tolerancia a fallos. Mientras más discos, más velocidad.
- Nivel 1: Mayor redundancia. Igual de rápido pero mucho más seguro. Usa duplicación de tipo espejo, hay demasiada redundancia.
- RAID 10: velocidad y tolerancia a fallos. Es el que ofrece mayor rendimiento. Soporta fallos en varias unidades simultáneamente. El total de discos debe ser par. Tiene un RAID 0 global, que utiliza un nnivel inferior de RAID 1.
- Nivel 5: acceso independiente con paridad distribuida. Permite utilizar hasta un 80% de los discos para almacenamiento, y el resto para paridad. Le asigna información de paridad a todos los discos. Es la solución más económica por megabyte



## Clase - Servicios DNS


- Un servidor DNS sirve para traducir nombres de dominio a direcciones IP's
- Utiliza el puerto 53, con UDP en vez de TCP. UDP es un protocolo no orientado a conexión


                nslookup google.com

## Clase - Introducción a la seguridad en redes de computadores

- Los elementos por orden de importancia son: los datos, el hardware y el software.
- Freenom: Para crear dominios  gratis
- Lets encrypt: genera los

## Proyecto Unidad 2 y 3


        docker run -ti --name db-prestashop--mysql --network prestashop-net -e MYSQL_ROOT_PASSWORD=admin -p 3307:3306 -d mysql:5.7

        sudo docker exec -it a8 /bin/bash
        rm -r install/



        http://localhost:8080/admin968yrpmbr/index.php?controller=AdminDashboard&token=7aae70713670ad33197489c01d00dc7e

        a2enmod ssl
        service apache2 restart


