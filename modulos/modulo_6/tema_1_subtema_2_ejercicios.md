# Ejercicios – Servicios y Escalamiento

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Tu primer servicio**
1. Asegúrate de estar en modo Swarm (`docker info` debe decir `Swarm: active`).
2. Crea un servicio simple:
   `docker service create --name pingpong --replicas 2 alpine ping 8.8.8.8`
3. Verifica su estado: `docker service ls` y `docker service ps pingpong`.
4. Deberías ver 2 tareas corriendo.

**Ejercicio 2 – Escalamiento manual**
1. Escala el servicio a 5 réplicas:
   `docker service scale pingpong=5`
2. Ejecuta `docker service ps pingpong` de nuevo. Verás las nuevas tareas iniciándose.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – auto-reparación**
1. Identifica el ID de uno de los contenedores reales del servicio `pingpong` usando `docker ps` (no `docker service ps`).
2. Mátalo sin piedad: `docker rm -f <container_id>`.
3. Rápidamente ejecuta `docker service ps pingpong`.
4. Verás una tarea marcada como `Failed` o `Shutdown` y una nueva tarea `Running` creada hace segundos para reemplazarla.

**Ejercicio 4 – Publicando puertos**
1. Crea un servicio Nginx accesible desde fuera:
   `docker service create --name web --publish 8080:80 --replicas 2 nginx:alpine`
2. Abre tu navegador en `http://localhost:8080`.
3. Refresca varias veces (si tuvieras una página que mostrara el hostname, verías cambiar el ID del contenedor que responde).

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Rolling Update en vivo**
1. Vamos a actualizar el servicio `web`.
2. Ejecuta `docker service update --image nginx:latest --update-parallelism 1 --update-delay 5s web`.
3. Observa el proceso con `docker service ps web` (o `watch docker service ps web` en Linux).
4. Verás cómo bajan versión `alpine` y suben versión `latest` una por una.

**Ejercicio 6 – Rollback**
1. Imagina que la nueva versión falló. Deshaz el cambio:
   `docker service rollback web`.
2. Swarm volverá a la configuración anterior (la imagen `nginx:alpine`).
