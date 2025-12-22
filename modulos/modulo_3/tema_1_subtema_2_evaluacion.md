# Evaluación – DNS y Descubrimiento de Servicios

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es la dirección IP del servidor DNS interno embebido en los contenedores Docker?**
   a) 127.0.0.1
   b) 8.8.8.8
   c) 127.0.0.11 *(Correcta)*
   d) 192.168.0.1

2. **Para que dos contenedores puedan resolver sus nombres por DNS, ¿qué requisito deben cumplir?**
   a) Estar en el mismo host físico.
   b) Estar conectados a la misma red definida por el usuario (user-defined network). *(Correcta)*
   c) Tener el mismo nombre de imagen.
   d) Usar el driver `none`.

3. **¿Qué es una VIP en el contexto de Docker Swarm?**
   a) Una persona muy importante.
   b) Una IP Virtual única que representa a un servicio y balancea tráfico a sus réplicas. *(Correcta)*
   c) Una IP variable que cambia cada segundo.
   d) La IP pública del nodo manager.

## Preguntas de Desarrollo (30 pts)

4. **Explica por qué no se recomienda usar direcciones IP estáticas (hardcoded) para comunicar contenedores.**
   *Rúbrica*: 10 pts por explicar que los contenedores son efímeros y pueden obtener diferentes IPs al reiniciarse o recrearse. Usar nombres DNS gestionados por Docker garantiza que la conexión siempre apunte al contenedor correcto independientemente de su IP actual.

5. **Describe cómo funciona el Round Robin DNS (DNSRR) en Docker.**
   *Rúbrica*: 10 pts por explicar que en modo DNSRR, el servidor DNS devuelve una lista de todas las IPs de los contenedores que forman el servicio, en lugar de una sola VIP. El cliente suele elegir una de la lista (o rotar), distribuyendo así la carga.

6. **¿Qué comando usarías para ver todos los detalles de una red, incluyendo qué contenedores están conectados y sus IPs?**
   *Rúbrica*: 10 pts por `docker network inspect <nombre_red>`.
