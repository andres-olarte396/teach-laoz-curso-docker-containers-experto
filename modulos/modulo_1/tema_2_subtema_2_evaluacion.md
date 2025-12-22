# Evaluación – Ciclo de vida básico

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué comando se utiliza para listar TODOS los contenedores, incluidos los detenidos?**
   a) `docker ps`
   b) `docker ps -a` *(Correcta)*
   c) `docker images`
   d) `docker info`

2. **¿Cuál es la diferencia principal entre `docker stop` y `docker kill`?**
   a) `stop` borra el contenedor, `kill` no.
   b) `stop` envía SIGTERM (cierre ordenado), `kill` envía SIGKILL (forzado). *(Correcta)*
   c) `kill` es solo para procesos Linux.
   d) No hay diferencia.

3. **Si ejecutas `docker run -d nginx`, ¿en qué estado queda el contenedor?**
   a) Pausado.
   b) Ejecutándose en primer plano (bloquea terminal).
   c) Ejecutándose en segundo plano (Detached). *(Correcta)*
   d) Exited.

## Preguntas de Desarrollo (30 pts)

4. **Explica la diferencia conceptual y práctica entre `docker run` y `docker start`.**
   *Rúbrica*: 10 pts por indicar que `run` crea un contenedor nuevo desde una imagen, mientras que `start` inicia uno ya existente (detenido).

5. **Describe para qué sirve `docker exec` y da un ejemplo de uso común.**
   *Rúbrica*: 10 pts por mencionar que permite ejecutar comandos en un contenedor activo (ej. abrir una shell, lanzar un script de mantenimiento).

6. **¿Qué sucede si ejecutas un contenedor con el flag `--rm`? ¿Cuándo es útil?**
   *Rúbrica*: 10 pts por explicar que el contenedor se elimina automáticamente al detenerse, útil para tareas efímeras o pruebas para no dejar basura.
