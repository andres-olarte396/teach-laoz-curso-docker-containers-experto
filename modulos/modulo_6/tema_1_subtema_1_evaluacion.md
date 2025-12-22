# Evaluación – Conceptos de Cluster

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué comando convierte un nodo Docker estándar en el primer Manager de un nuevo Swarm?**
   a) `docker cluster start`
   b) `docker swarm init` *(Correcta)*
   c) `docker run swarm`
   d) `dockerd --mode=cluster`

2. **¿Cuál es la función del "Routing Mesh" en Docker Swarm?**
   a) Enrutar correos electrónicos.
   b) Permitir que cualquier nodo del clúster reciba tráfico en un puerto publicado y lo redirija transparente al nodo correcto que tiene el contenedor. *(Correcta)*
   c) Conectar los cables de red físicamente.
   d) Filtrar paquetes maliciosos.

3. **Para mantener la alta disponibilidad y el quórum (consenso) en caso de fallos, ¿cuántos Managers se recomienda tener en producción?**
   a) Número par (2, 4).
   b) Número impar (3, 5, 7). *(Correcta)*
   c) Solo 1.
   d) Tantos como Workers.

## Preguntas de Desarrollo (30 pts)

4. **Explica la diferencia de responsabilidades entre un nodo Manager y un nodo Worker.**
   *Rúbrica*: 10 pts por explicar que el Manager mantiene el estado del clúster, programa las tareas (scheduler) y maneja la API, mientras que el Worker solo ejecuta las tareas (contenedores) asignadas sin participar en las decisiones de orquestación.

5. **Si ejecutas `docker node update --availability drain <nodo>`, ¿qué sucede con los contenedores que estaban corriendo en ese nodo?**
   *Rúbrica*: 10 pts por explicar que Swarm detiene esos contenedores en el nodo drenado y los reprograma (recrea) en otros nodos disponibles del clúster que tengan estado "Active".

6. **¿Por qué un Worker no puede ejecutar comandos como `docker node ls` o `docker service create`?**
   *Rúbrica*: 10 pts por explicar que, por diseño de seguridad, los Workers no tienen acceso a la base de datos Raft ni a la API de gestión del clúster. Solo los Managers tienen las llaves del reino para evitar que un worker comprometido destruya el clúster.
