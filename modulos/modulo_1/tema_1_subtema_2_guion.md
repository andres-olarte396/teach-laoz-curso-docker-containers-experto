# Guión de Audio – Arquitectura Docker Engine

## Metadata
- **Duración estimada**: 4 minutos
- **Tono**: Didáctico, claro, motivador
- **Audiencia**: Desarrolladores de software con conocimientos básicos de contenedores

## INTRO (30 s)
¡Hola! En este subtema vamos a profundizar en la arquitectura interna del Docker Engine, el motor que hace posible crear y ejecutar contenedores de forma eficiente.

## DESARROLLO (2 min)

### 1️⃣ Docker Daemon (`dockerd`)
El daemon es un proceso de fondo que gestiona todos los objetos Docker: contenedores, imágenes, redes y volúmenes. Escucha peticiones a través de un socket Unix (`/var/run/docker.sock`) o TCP.

### 2️⃣ Docker Client (`docker`)
El cliente es la interfaz de línea de comandos que utilizamos habitualmente. Cada vez que ejecutas `docker build`, `docker run`, etc., el cliente envía una solicitud al daemon mediante el socket mencionado.

### 3️⃣ Docker Registry
El registry almacena y distribuye imágenes Docker. Puede ser público (Docker Hub) o privado (tu propio registro). Cuando haces `docker pull` o `docker push`, el daemon se comunica con el registry para descargar o subir imágenes.

### 4️⃣ Flujo típico de trabajo
1. **Build** – `docker build` → el cliente pide al daemon que compile una imagen a partir de un Dockerfile.
2. **Push** – `docker push` → la imagen se envía al registry.
3. **Pull** – `docker pull` → otros hosts descargan la imagen.
4. **Run** – `docker run` → el daemon crea y ejecuta un contenedor basado en esa imagen.

## CIERRE (30 s)
Conocer estos componentes te permite diagnosticar problemas, optimizar builds y diseñar pipelines CI/CD más robustos. ¡Ahora estás listo para poner en práctica lo aprendido!

## NOTAS DE PRODUCCIÓN
- Insertar pausa de 1 s después de cada sección.
- Resaltar palabras clave como *daemon*, *client* y *registry* con entonación ligeramente más alta.
