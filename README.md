# Tarea06_SXE

Aqui saque toda la informacion:

https://devdocs.prestashop-project.org/9/basics/installation/environments/docker/#use-docker-compose-to-manage-your-stack



## Paso 1

<img width="209" height="117" alt="image" src="https://github.com/user-attachments/assets/e1b07027-4ee7-4527-88ed-0a5aa3dcc1a1" />

Creamos un fichero llamado ```docker-compose.yml``` dentro de Idea y definimos los servicios ```PrestaShop```, ```db``` y ```PhPMyAdmin```. Tambien hice un fichero ```.env``` para guardar la informacion sensible del ```docker-compose.yml```


### PrestaShop

<img width="381" height="439" alt="image" src="https://github.com/user-attachments/assets/80491eb5-b768-4726-8b5a-f1d03a88afe4" />

De primero definimos que version de ```PrestaShop``` queremos que en este caso es la 8.1 (Docker va a descargar esta imagen si no la tienes localmente). En ```depend_on``` hacemos que dependa de ```db``` y exponemos el puerto ```80``` del contenedor en el puerto ```8080``` de nuestra máquina local.

- ```DB_SERVER: db``` > dirección del servidor de la base de datos. Como ambos servicios están en la misma red de Docker, podemos usar el nombre del servicio db
- ```DB_NAME: ${MYSQL_DATABASE}``` > nombre de la base de datos que PrestaShop va a usar. Se toma del archivo .env
- ```DB_USER: ${MYSQL_USER}``` > usuario de la base de datos que PrestaShop va a usar.
- ```DB_PASSWD: ${MYSQL_PASSWORD}``` > contraseña del usuario de la base de datos
- ```PS_INSTALL_AUTO: 1``` > indica que PrestaShop debe instalarse automáticamente sin intervención manual
- ```PS_LANGUAGE: es``` > idioma de la tienda que en este caso es español
- ```PS_COUNTRY: ES``` > país de la tienda que en este caso tambien es españa
- ```PS_DOMAIN: localhost:8080``` > dominio donde la tienda estará disponible. Es importante para generar URLs internas correctas
- ```ADMIN_MAIL: ${ADMIN_MAIL}``` > correo del administrador de la tienda
- ```ADMIN_PASSWD: ${ADMIN_PASSWORD}``` > contraseña del administrador


### PhPMyAdmin

<img width="386" height="344" alt="image" src="https://github.com/user-attachments/assets/e800287d-6fc0-4571-aa33-6229885fe178" />

Aqui en este caso le dice a Docker que use la imagen oficial de ```PhPMyAdmin``` y en ```depend_on``` es lo mismo que en el ```PrestaShop```. El puerto en este caso use la ```8082``` porque la 8081 estaba ocupada, otra cosa importante es que al buscar el localhost no se usa /es , aquí solo funciona con /

- ```PMA_HOST: db``` > host donde se encuentra la base de datos. Como ambos contenedores (phpmyadmin y db) están en la misma red Docker, podemos usar el nombre del servicio db.
- ```PMA_USER: ${MYSQL_USER}``` > usuario de la base de datos con el que phpMyAdmin se conectará.
- ```PMA_PASSWORD: ${MYSQL_PASSWORD}``` > contraseña del usuario de la base de datos.



## Paso 2

<img width="409" height="213" alt="image" src="https://github.com/user-attachments/assets/374bb877-5a87-4fe8-b1c9-5329284f9536" />

Usamos volumes para guardar los datos en caso de que se pierdan y lo usamos tanto en db como en prestashop. En cambio en PhPMyAdmin no es necesario ya que es solo una interfaz grafica y no se guardan datos.

_

<img width="402" height="199" alt="image" src="https://github.com/user-attachments/assets/37afc177-8fc8-47db-8eb8-f460d9ec3e9d" />

Use $(dato a ingresar) para que las contraseñas, user, etc sean llamadas desde el ```.env``` en vez de volver a escribir todos los datos de nuevo en el ```docker-compose.yml```



## Paso 3

<img width="781" height="111" alt="image" src="https://github.com/user-attachments/assets/c78de133-d484-4d79-985f-5c3dbf247954" />

Agregamos un ```healthcheck``` solo a ```db``` para que los servicios sepan cuando arrancar y que se monitoree la salud continua del servicio (para comprobar que el servidor este operativo) (no es necesario en ```PrestaShop``` y ```PhPMyAdmin``` ya que ```db``` engloba los dos al ser la base de datos central ദ്ദി ˉ͈̀꒳ˉ͈́ )✧)

Tuve problemas para que la base da datos pillara mi contraseña del root asi que lo agregue directamente en el ```healthcheck```. El ```-uroot``` es para indicar al ususario con el que mysqladmin se conectara



## Paso 4

<img width="311" height="79" alt="imagen" src="https://github.com/user-attachments/assets/987439bf-83d1-483e-85d7-7f1690e82bbe" />

Añadimos dentro de ```depend_on > bd > condition: service_healthy``` para que espere a que el ```healthcheck``` sea correcto



## Paso 5

<img width="1152" height="236" alt="image" src="https://github.com/user-attachments/assets/a35624cb-908a-47a3-8f5b-eadcce16f5aa" />

Teniendo todo ya completado usamos el comando ```docker compose up``` para desplegarlo y seguidamente comprobamos en nuestro localhost que funciona 




## Resultado

<img width="1640" height="859" alt="image" src="https://github.com/user-attachments/assets/bf09eb17-2912-470c-9058-194303bc4c34" />

<img width="1620" height="653" alt="image" src="https://github.com/user-attachments/assets/898d6266-07db-4ec3-aa8d-4cca4927a2b3" />

