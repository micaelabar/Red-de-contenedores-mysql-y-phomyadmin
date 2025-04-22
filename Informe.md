# Red de contenedores mysql y phomyadmin

## 1. Tiempo de duración:
Duración estimada de la práctica: 2 horas.
## 2. Fundamentos:
En esta práctica se abordan conceptos clave de virtualización ligera mediante contenedores Docker, enfocados en servicios de bases de datos (MySQL) y su administración mediante una interfaz web (phpMyAdmin).

Docker es una plataforma de contenedores que permite ejecutar aplicaciones de forma aislada, rápida y replicable. MySQL es un sistema de gestión de bases de datos relacional ampliamente utilizado, mientras que phpMyAdmin es una aplicación web que facilita la administración de bases de datos MySQL a través de una interfaz gráfica.

Los objetivos de esta actividad incluyen aprender a crear contenedores individuales con servicios que interactúan entre sí, configurar redes personalizadas en Docker, y validar la correcta comunicación entre los contenedores a través de la creación de una base de datos de prueba. Esta práctica representa un paso esencial hacia el desarrollo de soluciones escalables en arquitecturas de microservicios.
## Conocimientos previos
- Uso básico de Docker (comandos como run, ps, network).
- Conocimiento general de bases de datos relacionales (MySQL).
- Conceptos básicos de redes (puertos, nombres de host).
- Familiaridad con el uso de terminal o consola.
## Objetivos a alcanzar
- Crear un contenedor para MySQL con credenciales configuradas.
- Crear un contenedor para phpMyAdmin conectado al contenedor MySQL.
- Establecer una red personalizada en Docker.
- Verificar la comunicación entre phpMyAdmin y MySQL.
- Crear una base de datos de prueba desde la interfaz phpMyAdmin.
## Equipo necesario
- Computador con sistema operativo Windows, macOS o Linux.
- Docker instalado y en funcionamiento.
- Navegador web moderno (Chrome, Firefox, Edge, etc.).
## Material de apoyo
- Documentación oficial de Docker: https://docs.docker.com/
- Guía de instalación de MySQL Docker: https://hub.docker.com/_/mysql
- Documentación de phpMyAdmin: https://hub.docker.com/r/phpmyadmin/phpmyadmin
## Procedimiento
### Paso 1. Crear un contenedor para MySQL
Puedes crear un contenedor para MySQL utilizando el siguiente comando en Docker:
```
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=rootpassword -d mysql:latest
````
## Evidencia:
<imag!
### Paso 2. Crear un contenedor para phpMyAdmin
A continuación, crea un contenedor para phpMyAdmin, asegurándote de que pueda comunicarse con el contenedor MySQL:
```
docker run --name phpmyadmin-container -d --link mysql-container:db -p 8080:80 phpmyadmin/phpmyadmin
````
## Evidencia:
<imag!
### Paso 3. Crear una red personalizada en Docker
Para que ambos contenedores puedan comunicarse, primero crea una red personalizada:
```
docker network create my_network
````
### Paso 4. Conectar ambos contenedores a la red: 
Conectamos los contenedores a la red personalizada:
```
docker network connect my_network mysql-container
````
```
docker network connect my_network phpmyadmin-container
````
## Evidencia:
<imag!
### Paso 5. Configurar la conexión entre phpMyAdmin y MySQL:
Accedemos a phpMyAdmin en el navegador (http://localhost:8080) y configuramos la conexión con las credenciales proporcionadas.
## Evidencia:
<imag!
### Paso 6. Crear una base de datos de prueba:
Desde phpMyAdmin, creamos una base de datos llamada testdb.
## Evidencia:
<imag!
### Resultados:


