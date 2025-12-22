# Evaluación – Instalación y Hola Mundo

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué comando se utiliza para verificar que Docker está instalado y corriendo correctamente mostrando ambas partes (Client y Server)?**
   a) `docker --help`
   b) `docker version` *(Correcta)*
   c) `docker info`
   d) `docker status`

2. **Al ejecutar `docker run hello-world` por primera vez, ¿qué mensaje indica que Docker está descargando la imagen de internet?**
   a) `Download complete`
   b) `Unable to find image 'hello-world:latest' locally` *(Correcta)*
   c) `Pulling from library/hello-world`
   d) `Error response from daemon`

3. **¿Qué herramienta se recomienda para instalar Docker en entornos de desarrollo Windows o Mac?**
   a) Docker Toolbox
   b) Docker Engine nativo
   c) Docker Desktop *(Correcta)*
   d) Compilar desde el código fuente

## Preguntas de Desarrollo (30 pts)

4. **Explica qué sucede paso a paso cuando ejecutas `docker run hello-world` y la imagen no está en tu máquina.**
   *Rúbrica*: 10 pts por describir:
   1. El cliente contacta al daemon.
   2. El daemon busca localmente, no la encuentra.
   3. Hace "pull" desde Docker Hub.
   4. Crea el contenedor a partir de la imagen descargada.
   5. Ejecuta el proceso dentro del contenedor y muestra la salida (StdOut).

5. **¿Por qué es necesario habilitar la virtualización (Hyper-V o WSL2) en Windows para usar Docker?**
   *Rúbrica*: 10 pts por explicar que los contenedores Linux necesitan un Kernel Linux para funcionar. Docker Desktop en Windows utiliza una máquina virtual ligera (o WSL2) para proveer este kernel, ya que Windows no lo tiene nativamente.

6. **¿Qué es Docker Hub?**
   *Rúbrica*: 10 pts por definirlo como el registro público predeterminado donde se alojan y comparten imágenes de contenedores.
