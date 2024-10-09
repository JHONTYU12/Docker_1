# COMPLETAR  
Comparando sus conocimientos antes de hacer la práctica con sus conocimientos después de hacer la tarea, explicar los principales aprendizajes logrados para beneficio de su formación profesional.  
Si solucionó un problema presentado al realizar la práctica también se debe documentar.

# Reflexión sobre los aprendizajes logrados

## Comparación de conocimientos antes y después de la práctica

Antes de realizar esta práctica, mi conocimiento de Docker y la ejecución de servicios complejos, como RabbitMQ, era limitado y estaba principalmente enfocado en la creación básica de contenedores y el mapeo de puertos. Sabía los conceptos teóricos, pero no había experimentado a fondo con contenedores para servicios complejos, la gestión de imágenes, el uso de capas de Docker, o la depuración de errores prácticos en la ejecución.

Después de completar la práctica, los principales aprendizajes que logré son:

### 1. **Capas de imágenes de Docker y su optimización**:
   - Aprendí que Docker utiliza un sistema de capas para almacenar imágenes de forma eficiente. Por ejemplo, vimos que **RabbitMQ** tiene varias capas, debido a que requiere muchas dependencias adicionales como **Erlang** y otras bibliotecas. 
   - También noté que **Nginx Alpine** es significativamente más ligero porque solo tiene unas pocas capas, lo que hace que la descarga y ejecución sean más rápidas.
   - El proceso de descarga de imágenes también varía en función de si una capa ya está almacenada en caché localmente, lo que optimiza la reutilización de recursos.

### 2. **Mapeo correcto de puertos**:
   - Un aprendizaje fundamental fue entender que los servicios dentro del contenedor exponen ciertos puertos que necesitan ser mapeados correctamente al host. Durante la práctica, cometí un error al mapear el puerto incorrecto de RabbitMQ, lo que me impidió acceder a la interfaz de administración.
   - Ahora entiendo que RabbitMQ expone su **consola de administración en el puerto 15672**, y que, para acceder desde el host, es necesario mapear este puerto a un puerto disponible en la máquina anfitriona.

### 3. **Gestión avanzada de contenedores**:
   - A través de la práctica, mejoré mi capacidad para gestionar contenedores. Aprendí a **detener**, **eliminar** y **renombrar** contenedores cuando se presentan conflictos, lo cual es esencial en entornos de desarrollo y producción.
   - También descubrí la importancia de usar nombres de contenedores únicos, para evitar errores de colisión y conflictos con nombres duplicados.

### 4. **Inspección y depuración de contenedores**:
   - La inspección de contenedores con el comando `docker inspect` se convirtió en una herramienta clave para revisar el estado, configuraciones, y detalles como los puertos expuestos, el ID de la imagen, las redes a las que está conectado y otros detalles críticos.
   - La inspección me permitió comprender mejor cómo interactúan los contenedores con el sistema y detectar errores de configuración rápidamente.

### 5. **Resolución de errores comunes**:
   - Durante la práctica, aprendí a resolver problemas comunes relacionados con el mapeo de puertos incorrectos, contenedores con nombres duplicados y errores de acceso a servicios desde el host. Cada problema me permitió mejorar mis habilidades de depuración y me dio confianza para gestionar sistemas más complejos.

## Solución de problemas presentados

### Problema 1: No poder acceder a la interfaz de administración de RabbitMQ

**Descripción**: Al intentar acceder a RabbitMQ en `http://localhost:9999`, la página no cargaba porque mapeé el puerto 9999 del host al puerto 9999 dentro del contenedor, en lugar de al puerto correcto, que es **15672**.

**Solución**:
- Utilicé el comando `docker ps` para revisar los puertos que estaban realmente expuestos en el contenedor y descubrí que el puerto 15672 es el correcto para la consola de administración.
- Corregí el comando de ejecución del contenedor para que el puerto **15672** del contenedor se mapee correctamente al puerto **9000** en mi host:

```bash
docker run -d --name Conejo -p 9000:15672 rabbitmq:management-alpine
```
## Problema 2: Conflicto de nombres de contenedores

**Descripción**: Al intentar crear un nuevo contenedor, recibí un error porque ya existía un contenedor con el nombre **Conejo2**. Esto ocurre porque Docker no permite nombres duplicados para los contenedores.

**Solución**:
- Detuve y eliminé el contenedor existente con el nombre duplicado:

```bash
docker stop Conejo2
docker rm Conejo2
```
## Conclusión

Durante esta práctica, mejoré significativamente mi capacidad para gestionar contenedores y servicios complejos como RabbitMQ en Docker. A través de la resolución de problemas relacionados con el mapeo de puertos, la descarga de imágenes grandes y la gestión de nombres de contenedores, adquirí un conocimiento más profundo sobre cómo funciona Docker y cómo interactúan los contenedores con el host.

Algunos de los aspectos clave que aprendí fueron:

1. **Gestión eficiente de imágenes**: Comprendí cómo Docker utiliza capas para optimizar la descarga y almacenamiento de imágenes, lo que reduce el tiempo y el uso de recursos al trabajar con varias instancias de contenedores.
   
2. **Mapeo correcto de puertos**: Aprendí a mapear correctamente los puertos entre el host y el contenedor, lo cual es esencial para acceder a servicios como RabbitMQ desde la máquina local.

3. **Diagnóstico y resolución de problemas**: Desarrollé la habilidad de diagnosticar y solucionar problemas comunes como el conflicto de nombres de contenedores y la configuración incorrecta de puertos, lo que mejoró mi capacidad para trabajar con Docker de manera más efectiva.

