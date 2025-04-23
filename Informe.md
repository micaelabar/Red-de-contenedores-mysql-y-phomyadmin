# Red de contenedores mysql y phomyadmin

## 1. Tiempo de duración:
Duración estimada de la práctica: 2 horas.
## 2. Fundamentos:
En esta práctica se abordan conceptos clave de virtualización ligera mediante contenedores Docker, enfocados en servicios de bases de datos (MySQL) y su administración mediante una interfaz web (phpMyAdmin).

Docker es una plataforma de contenedores que permite ejecutar aplicaciones de forma aislada, rápida y replicable. MySQL es un sistema de gestión de bases de datos relacional ampliamente utilizado, mientras que phpMyAdmin es una aplicación web que facilita la administración de bases de datos MySQL a través de una interfaz gráfica.

Los objetivos de esta actividad incluyen aprender a crear contenedores individuales con servicios que interactúan entre sí, configurar redes personalizadas en Docker, y validar la correcta comunicación entre los contenedores a través de la creación de una base de datos de prueba. Esta práctica representa un paso esencial hacia el desarrollo de soluciones escalables en arquitecturas de microservicios.
## Conocimientos previos:
- Uso básico de Docker (comandos como run, ps, network).
- Conocimiento general de bases de datos relacionales (MySQL).
- Conceptos básicos de redes (puertos, nombres de host).
- Familiaridad con el uso de terminal o consola.
## Objetivos a alcanzar:
- Crear un contenedor para MySQL con credenciales configuradas.
- Crear un contenedor para phpMyAdmin conectado al contenedor MySQL.
- Establecer una red personalizada en Docker.
- Verificar la comunicación entre phpMyAdmin y MySQL.
- Crear una base de datos de prueba desde la interfaz phpMyAdmin.
## Equipo necesario:
- Computador con sistema operativo Windows, macOS o Linux.
- Docker instalado y en funcionamiento.
- Navegador web moderno (Chrome, Firefox, Edge, etc.).
## Material de apoyo:
- Documentación oficial de Docker: https://docs.docker.com/
- Guía de instalación de MySQL Docker: https://hub.docker.com/_/mysql
- Documentación de phpMyAdmin: https://hub.docker.com/r/phpmyadmin/phpmyadmin
## Procedimiento:
### Paso 1. Abrir la terminal en Ubuntu.
Ejecutar el siguiente comando para crear un contenedor de MySQL. En este ejemplo, configuramos las credenciales necesarias (MYSQL_ROOT_PASSWORD, MYSQL_DATABASE y MYSQL_USER):
```
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=mi_contraseña -e MYSQL_DATABASE=mi_base_de_datos -e MYSQL_USER=mi_usuario -e MYSQL_PASSWORD=mi_password -d mysql:latest
````
## Evidencia:
<imag!![imagen 1](https://github.com/user-attachments/assets/13c0c624-00d1-4ab8-87ee-b752c786d9ef)

### Paso 2. Verificar que el contenedor esté en funcionamiento.
```
docker ps
````
## Evidencia:
<imag!![imagen 2](https://github.com/user-attachments/assets/f37737ff-8e32-4c2e-9fd5-0d1a53545813)

### Paso 3. Crear un contenedor para phpMyAdmin.
Ejecutar el siguiente comando para crear un contenedor de phpMyAdmin. Conectamos phpMyAdmin al contenedor de MySQL mediante variables de entorno:
```
docker run --name phpmyadmin-container --link mysql-container:db -p 8080:80 -d phpmyadmin/phpmyadmin
````
## Evidencia:
<imag!![imagen 3](https://github.com/user-attachments/assets/e43132df-002a-4bbc-871c-d8986f888f80)

### Paso 4. Verificar que el contenedor phpMyAdmin esté funcionando.
Esto debe mostrar que el contenedor phpmyadmin-container está en ejecución.
```
docker ps
````
## Evidencia:
<imag!![imagen 4](https://github.com/user-attachments/assets/ffb1aa13-e266-44cc-b516-e4dee11739f0)

### Paso 5. Crear una red personalizada en Docker.
Crear una red personalizada para que los contenedores puedan comunicarse entre sí de manera segura:
```
docker run --name phpmyadmin-v2 --network my-network -p 8081:80 -e PMA_HOST=mysql-container -d phpmyadmin/phpmyadmin
````
## Evidencia:
<imag!![imagen 5](https://github.com/user-attachments/assets/60e1f263-0e9b-4cc6-bb2d-4d6979e69000)

### Paso 6. Conectar ambos contenedores a la red.
```
docker network connect my-network mysql-container
````
```
docker network connect my-network phpmyadmin-v2
````
## Evidencia:
<imag!![imagen 6](https://github.com/user-attachments/assets/ad77e1c9-a63c-432d-8d3b-aae42a9117ad)

### Paso 7. Configurar la conexión entre phpMyAdmin y MySQL.
Acceder a phpMyAdmin. Abre un navegador web y accede a:
```
http://localhost:8081
````
## Evidencia:
<imag!![imagen 7](https://github.com/user-attachments/assets/8080b19c-c419-4f5b-a64d-1fbf4393e4fd)

### Paso 8. Crear una base de datos de prueba.
1. Una vez dentro de la interfaz de phpMyAdmin, crear una base de datos de prueba:
2. Haz clic en "Bases de datos" en el menú superior.
3. Escribe un nombre para la base de datos, por ejemplo, test_db.
4. Haz clic en "Crear".
## Evidencia:
<imag!![imagen 8](https://github.com/user-attachments/assets/71ce6cf0-ea04-4a40-a278-f2c9b9eba120)

### Resultados:
Verifica que la base de datos se haya creado correctamente .
## Evidencia:
<imag!![imagen 9](https://github.com/user-attachments/assets/ab23a250-1214-4fa2-b0d3-585e9e604621)

Código SQL para crear una base de datos de prueba.
## Evidencia:
<imag!![resultado](https://github.com/user-attachments/assets/9b684239-bf95-4471-912a-3ed5f474b798)

### Conclusión:
En esta práctica se logró configurar con éxito un entorno de base de datos utilizando contenedores Docker, demostrando la eficiencia y facilidad que ofrece esta herramienta para el despliegue de servicios. Se crearon dos contenedores: uno para MySQL y otro para phpMyAdmin, configurando sus credenciales adecuadamente. Además, se implementó una red personalizada para permitir la comunicación segura entre ambos servicios. A través de la interfaz de phpMyAdmin, se verificó la conexión con el contenedor de MySQL y se creó una base de datos de prueba. Esta actividad fortaleció el conocimiento práctico sobre contenedores, redes personalizadas en Docker y la gestión de bases de datos de manera eficiente y portátil, lo cual es esencial en entornos modernos de desarrollo y despliegue de aplicaciones.


