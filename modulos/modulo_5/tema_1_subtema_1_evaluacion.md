# Evaluación – Seguridad del Docker Daemon

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué riesgo implica montar `/var/run/docker.sock` dentro de un contenedor?**
   a) El contenedor se vuelve más lento.
   b) El contenedor obtiene control total sobre el daemon Docker, pudiendo crear/destruir cualquier contenedor y montar volúmenes del host. *(Correcta)*
   c) Se duplica el espacio en disco.
   d) Ninguno, es una práctica estándar segura.

2. **¿Cuál es el puerto estándar NO SEGURO para la API remota de Docker?**
   a) 2375 *(Correcta)*
   b) 2376
   c) 8080
   d) 22

3. **¿Qué hace la opción `"userns-remap": "default"` en `daemon.json`?**
   a) Mapea los puertos del host a los contenedores automáticamente.
   b) Reasigna los UIDs del contenedor a un rango de UIDs no privilegiados en el host, de modo que root en el contenedor no sea root en el host. *(Correcta)*
   c) Cambia el nombre de usuario del administrador.
   d) Desactiva la red.

## Preguntas de Desarrollo (30 pts)

4. **Explica por qué dar acceso al grupo `docker` a un usuario equivale a darle acceso `root` sin contraseña.**
   *Rúbrica*: 10 pts por explicar que el usuario puede ejecutar `docker run -v /:/host alpine sh` y obtener acceso de escritura inmediato a todo el sistema de archivos del host con privilegios de root, pudiendo modificar `/etc/shadow`, instalar backdoors, etc.

5. **Menciona dos configuraciones de seguridad recomendadas para agregar en `/etc/docker/daemon.json`.**
   *Rúbrica*: 10 pts por mencionar dos de: `"no-new-privileges": true`, `"live-restore": true`, `"userns-remap"`, `"icc": false` (inter-container communication desactivada por defecto), o configuración de logs.

6. **Si necesitas administrar un servidor Docker remoto de forma segura, ¿cuál es la alternativa moderna y sencilla al setup complejo de TLS?**
   *Rúbrica*: 10 pts por mencionar el uso de **SSH** (`docker context create ... host=ssh://...`). Docker CLI soporta nativamente la conexión al socket remoto a través de un túnel SSH, aprovechando la autenticación y encriptación existente de SSH.
