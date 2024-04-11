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
docker build -t <nombre_de_la_imagen> .
``` 
Donde `<nombre_de_la_imagen>` es el nombre que quieras darle a la imagen.

## 2. Creación de la infraestructura con Terraform
A continuación crearemos la infraestructura necesaria para ejecutar la aplicación, que consta de:

- El contenedor de Jenkins a partir de la imagen creada anteriormente.

- Un contenedor de Docker in Docker necesario para Jenkins.

- Una red de Docker llamada jenkins para comunicar ambos contenedores.
- Un par de volúmenes, uno para los datos de Jenkins y otro para los certificados TLS.