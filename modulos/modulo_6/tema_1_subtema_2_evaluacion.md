# Evaluación – Servicios y Escalamiento

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué comando se utiliza para cambiar el número de réplicas de un servicio en ejecución?**
   a) `docker service update --replicas`
   b) `docker service scale` *(Correcta)*
   c) `docker container multiply`
   d) `docker swarm resize`

2. **¿Qué sucede si eliminas manualmente (`docker rm`) un contenedor que pertenece a un servicio Swarm?**
   a) El servicio queda con una réplica menos permanentemente.
   b) Swarm detecta la discrepancia con el estado deseado y crea un nuevo contenedor para reemplazarlo. *(Correcta)*
   c) Se elimina todo el servicio.
   d) El nodo se apaga.

3. **Durante un "Rolling Update", ¿cuál es el comportamiento por defecto de Swarm?**
   a) Detiene todos los contenedores viejos a la vez y luego inicia los nuevos.
   b) Actualiza los contenedores uno a uno (o en grupos pequeños), esperando a que estén activos antes de continuar con el siguiente. *(Correcta)*
   c) Crea un clúster paralelo.
   d) No hace nada, debes hacerlo manualmente.

## Preguntas de Desarrollo (30 pts)

4. **Explica la diferencia conceptual entre un "Servicio" (`docker service`) y un "Contenedor" (`docker run`).**
   *Rúbrica*: 10 pts por explicar que un contenedor es una instancia aislada efímera, mientras que un servicio es la definición del estado deseado (imagen, configuración, número de réplicas) que el orquestador se encarga de mantener permanentemente a través de múltiples contenedores (tasks).

5. **Describe qué es el "Routing Mesh" y cómo facilita el acceso a un servicio escalado.**
   *Rúbrica*: 10 pts por explicar que permite enviar tráfico a cualquier nodo del clúster en el puerto publicado, y Swarm se encarga de enrutar ese tráfico internamente hacia un contenedor válido del servicio, actuando como un balanceador de carga transparente.

6. **Si despliegas una actualización defectuosa que rompe tu aplicación, ¿qué comando te permite volver rápidamente al estado anterior funcional?**
   *Rúbrica*: 10 pts por `docker service rollback <nombre_servicio>`.
