# Imagen
Es un archivo único que contiene todos los programas, librerías, dependencias y configuraciones necesarias para instalar y/o ejecutar una aplicación o un conjunto de aplicaciones.
![Imagen](img/imagen.PNG)


## ¿Cuál es la relación entre una imagen y un contenedor? 
### IMAGEN
- Es el molde que contiene todo lo que necesita una aplicacion para ejecutarse
- No se puede cambiar una vez que fue creado
### CONTENEDOR
- Instancia de una imagen que esta en ejecuccion
- Se puede realizar cambios pero si no se guarda en **Volumenes** al momento de borrar se pierde
### RELACION DE AMBOS
- Primero creas la imagen (en maquina o en DockerHub)
- Al usar la imagen Docker lo convierte en un contenedor

![Imagen y contenedores](img/imagenContenedores.JPG)
## Comandos para imágenes

### Descargar imagen
Descarga la última versión de la imagen disponible en el registro de Docker.

```
docker pull <nombre imagen> 
```

Descarga una versión específica de la imagen, cada imagen tiene etiquetas (tags) para diferentes versiones.
Una imagen puede tener la etiqueta latest para representar la última versión, si no se especifica una etiqueta se hará referencia a la versión latest.

```
docker pull <nombre imagen>:<tag>
```

Descargar la imagen **hello-world**.

**1: Sin tag**
```
docker pull hello-world**
```
**2: Con tag** (Ultima version)
```
**docker pull hello-world:latest**
```

**¿Qué es nginx**

NGINX es un servidor web de código abierto que mejora la eficiencia de los sitios web al:

- **Servir Contenido Web:** Entrega páginas, imágenes y archivos a los visitantes.
- **Manejar Tráfico:** Organiza múltiples solicitudes simultáneas para evitar tiempos de espera.
- **Actuar como Proxy Inverso:** Redirige solicitudes a diferentes servidores donde se encuentran los componentes del sitio.
- **Equilibrar Carga:** Distribuye las solicitudes entre varios servidores para mantener el rendimiento durante picos de tráfico.
- **Ser Rápido y Eficiente:** Diseñado para manejar muchas conexiones al mismo tiempo sin volverse lento.

Descargar la imagen  **nginx** en la versión **alpine**
```
docker pull nginx:alpine
```
### Listar imágenes
```
docker images
```
## Screen de resultados
Imagen de resultados:

![Screen de Listas de imagenes](img/ScreenImagenList.png)

**Identificadores**

En Docker, se utilizan varios identificadores para diferenciar de manera única los elementos del sistema, como imágenes, contenedores, volúmenes y redes. Estos identificadores son generados automáticamente por Docker y son únicos dentro del contexto del sistema Docker en el que se encuentran. 

### Inspeccionar una imagen
El comando docker inspect se utiliza para obtener información detallada sobre un objeto de Docker específico, como un contenedor, una imagen, un volumen o una red.  Proporciona información en formato JSON sobre el objeto especificado.

```
docker inspect <nombre imagen>
docker inspect <nombre imagen>:<tag>
```

Inspeccionar la imagen hello-world 
# COMPLETAR

**¿Con qué algoritmo se está generando el ID de la imagen**
# COMPLETAR

### Filtrar imágenes

```
docker images | grep <termino a buscar>

```

### Para eliminar una imagen
Eliminar permanentemente la imagen de tu sistema Docker.

```
docker rmi <nombre imagen>:<tag>
```

Eliminar la imagen hello-world 
# COMPLETAR

-f: Es la opción para forzar la eliminación de la imagen incluso si hay contenedores en ejecución que utilizan esa imagen.
Cuando eliminas una imagen Docker, Docker no elimina automáticamente los contenedores que se han creado a partir de esa imagen. Esto significa que, aunque hayas eliminado la imagen, el contenedor seguirá ejecutándose normalmente.  
**Considerar**
Eliminar una imagen no afecta a los contenedores que se han creado a partir de esa imagen, a menos que esos contenedores dependan de archivos o configuraciones específicas de la imagen eliminada. En ese caso, es posible que los contenedores se comporten de manera inesperada después de eliminar la imagen.
Es una buena práctica detener y eliminar todos los contenedores que dependan de una imagen antes de eliminar la imagen en sí.

```
docker rmi -f <nombre imagen>:<tag>
```

