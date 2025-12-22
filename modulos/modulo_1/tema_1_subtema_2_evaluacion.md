# Evaluación – Arquitectura Docker Engine

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es el componente de Docker que se ejecuta como un proceso en segundo plano (daemon) y gestiona los objetos de Docker?**
   a) Docker Client
   b) Docker Daemon (dockerd) *(Correcta)*
   c) Docker Registry
   d) Docker Compose

2. **¿Qué comando permite al cliente de Docker comunicarse con el daemon?**
   a) API REST *(Correcta)*
   b) SSH
   c) FTP
   d) Telnet

3. **¿Dónde se almacenan las imágenes de Docker por defecto si no se encuentran localmente?**
   a) En el Docker Daemon
   b) En el Docker Client
   c) En un Docker Registry (como Docker Hub) *(Correcta)*
   d) En la memoria RAM

## Preguntas de Desarrollo (30 pts)

4. **Explica brevemente la diferencia entre una Imagen y un Contenedor.**
   *Rúbrica*: 10 pts por mencionar que la Imagen es la plantilla de solo lectura (el "clase" en POO) y el Contenedor es la instancia ejecutable de esa imagen (el "objeto").

5. **Describe el flujo de la arquitectura Cliente-Servidor de Docker cuando ejecutas `docker run nginx`.**
   *Rúbrica*: 10 pts por explicar:
   1. El Cliente (CLI) envía la orden a la API.
   2. El Daemon recibe la orden.
   3. El Daemon busca la imagen localmente; si no la tiene, la descarga del Registry.
   4. El Daemon crea y arranca el contenedor.

6. **¿Qué son los Namespaces en el contexto de la tecnología subyacente de Docker?**
   *Rúbrica*: 10 pts por explicar que proporcionan aislamiento. Permiten que un contenedor tenga su propia vista del sistema (PID, Network, Mount), haciendo que crea que es el único proceso corriendo en la máquina.
