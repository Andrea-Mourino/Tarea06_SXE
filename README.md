# Tarea06_SXE

Aqui saque toda la informacion:

https://devdocs.prestashop-project.org/9/basics/installation/environments/docker/#use-docker-compose-to-manage-your-stack



## Paso 1

<img width="225" height="116" alt="imagen" src="https://github.com/user-attachments/assets/a8ae01e4-db7b-4d59-a5ca-4373267d1c38" />

Creamos un fichero llamado docker-compose.yml dentro de Idea y definimos los  servicios prestashop, db y PhPMyAdmin. Tambien hice un fichero info.env para guardar la informacion sensible del docker-compose.yml



## Paso 2

<img width="465" height="411" alt="imagen" src="https://github.com/user-attachments/assets/93649e97-82a2-4af2-a151-04f402f4134e" />

Usamos volumes para guardar los datos en caso de que se pierdan y lo usamos tanto en db como en prestashop. En cambio en PhPMyAdmin no es necesario ya que es solo una interfaz grafica y no se guarda datos.

_

<img width="320" height="484" alt="imagen" src="https://github.com/user-attachments/assets/a6e4bf95-5194-43ae-9f01-dc5220878a82" />

Use $(dato a ingresar) para que las contraseñas, user, etc lo llame desde el info.env en vez de volver a escribir todos los datos de nuevo en el docker-compose.yml



## Paso 3

<img width="603" height="269" alt="Captura desde 2025-10-17 09-27-33" src="https://github.com/user-attachments/assets/8f1388a5-eb2d-4f92-a78a-ee376095087c" />

Teniendo todo creado usamos el comando docker compose up para desplegarlo

