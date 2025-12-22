# Evaluación – Development vs Production

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **Si tienes un `docker-compose.yml` y un `docker-compose.override.yml` en la misma carpeta, ¿qué sucede al ejecutar `docker compose up`?**
   a) Docker ignora el override.
   b) Docker usa solo el override.
   c) Docker fusiona ambos archivos, dando prioridad a las configuraciones del override. *(Correcta)*
   d) Docker muestra un error de conflicto.

2. **¿Cuál comando usarías para levantar tu stack usando una configuración específica de producción?**
   a) `docker compose up --production`
   b) `docker compose -f docker-compose.yml -f docker-compose.prod.yml up` *(Correcta)*
   c) `docker compose use production`
   d) `docker compose up` (Docker adivina que es producción).

3. **¿Para qué sirven los `profiles` en Docker Compose?**
   a) Para definir perfiles de usuario y contraseñas.
   b) Para agrupar servicios que solo deben iniciarse bajo demanda (ej. herramientas de debug). *(Correcta)*
   c) Para optimizar el rendimiento de la CPU.
   d) Para cambiar el color de la terminal.

## Preguntas de Desarrollo (30 pts)

4. **Explica por qué es una buena práctica usar un bind mount (`./src:/app/src`) en el archivo override de desarrollo pero NO en producción.**
   *Rúbrica*: 10 pts por explicar que en desarrollo permite "hot-reload" (ver cambios de código al instante), mientras que en producción queremos inmutabilidad y consistencia, por lo que debemos usar el código copiado dentro de la imagen (`COPY . .`) durante el build, evitando depender de archivos externos del host.

5. **Describe cómo funciona la fusión (merge) de configuraciones en Compose. Si el archivo base define `ports: ["80:80"]` y el override define `ports: ["8080:80"]`, ¿cuál gana?**
   *Rúbrica*: 10 pts por explicar que Compose fusiona las listas o sobrescribe claves escalares. En el caso de puertos (listas), si no se especifican estrategias de merge complejas, generalmente se agregan o sobrescriben dependiendo de la versión, pero el concepto clave es que la configuración del último archivo especificado con `-f` (o el override por defecto) tiene precedencia en caso de conflicto de valores únicos. *Nota técnica: Las listas suelen concatenarse en versiones antiguas, pero idealmente se debe pensar en que el override "gana" o complementa.*

6. **Menciona tres diferencias típicas entre una configuración de servicio en Dev vs Prod.**
   *Rúbrica*: 10 pts por mencionar 3 de:
   - Restart policy (`no` vs `always`).
   - Puertos (`bind` a localhost vs público).
   - Volúmenes (código montado vs imagen estática).
   - Variables de entorno (debug on vs off).
   - Logging (consola vs json-file/syslog).
