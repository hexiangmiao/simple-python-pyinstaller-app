# Instrucciones para el proceso de despliegue de la aplicación Python con Jenkins
En este archivo encontrará las instrucciones para desplegar la aplicación Python utilizando Jenkins.

## 0. Pasos previos

Antes de realizar nada, será necesario:

-  Un macOS, Linux, Windows, or Chromebook (con Linux) con:

    - 2 GB de RAM

    - 2 GB de espacio libre en el disco para Jenkins

- Tener el siguiente software instalado en su sistema:

    - Docker

    - Docker Compose

    - Terraform

- Descargar todos los archivos de este repositorio o clonarlo localmente (requiere tener Git instalado)


## 1. Creación de la imagen de Jenkins
Para crear la imagen de Jenkins, será necesario acceder desde la terminal al directorio donde hayas puesto el Dockerfile que se encuentra en el directorio ` docs ` del repositorio e introducir el siguiente comando: 
```bash
docker build -t myjenkins-blueocean .
``` 
Es importante ponerle exactamente ese nombre y no otro, puesto que es el nombre que usará el archivo de configuración de Terraform para crear el contenedor.

## 2. Creación de la infraestructura con Terraform
A continuación crearemos la infraestructura necesaria para ejecutar la aplicación, que consta de:

- El contenedor de Jenkins a partir de la imagen creada anteriormente.

- Un contenedor de Docker in Docker necesario para Jenkins.

- Una red de Docker llamada jenkins para comunicar ambos contenedores.

- Un par de volúmenes, uno para los datos de Jenkins y otro para los certificados TLS.

Crearemos la infraestructura utilizando terraform, realizando los siguientes pasos:

1. Nos situamos desde una terminal en el directorio donde hayamos puesto el archivo `main.tf` y ejecutamos: `terraform init`.
2. Una vez terraform se ha inicializado correctamente ejecutamos `terraform apply` y confirmamos escribiendo `yes`.

Con esto la infraestructura se habría creado correctamente y ya estariamos listos para configurar Jenkins.

## 3. Configuración de Jenkins

Ahora procederemos a configurar jenkins:

1. Accedemos a Jenkins en [localhost:8080](localhost:8080).
2. Nos pedirá que introduzcamos la contraseña de administrador, para ello ejecutamos en nuestra terminal `docker logs jenkins-blueocean`. Nos aparecerán los logs del contenedor de jenkins, encontraremos nuestra contraseña a continuación del texto que dice:
```bash
Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

<contraseña>
```
3. Una vez hemos introducido la contraseña, seleccionamos la opción 'Install suggested plugins' y esperamos a que se instalen.
4. Al terminar la instalación de los plugins, nos pedirá que creemos nuestro primer usuario administrador, así que introducimos el usuario y contraseña que queramos, así como un nombre y un correo electrónico.

Con esto habríamos terminado de configurar Jenkins.