# Evaluación – Drivers de Red

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué ventaja principal ofrece crear una red `bridge` definida por el usuario (custom bridge) frente a usar la red `bridge` por defecto?**
   a) Mayor velocidad de transmisión.
   b) Resolución de DNS automática (Service Discovery) entre contenedores. *(Correcta)*
   c) Acceso directo a la tarjeta de red del host.
   d) Cifrado de datos por defecto.

2. **Si necesitas que tu contenedor tenga una dirección IP real accesible directamente desde tu red LAN física (sin NAT), ¿qué driver usarías?**
   a) Bridge.
   b) Host.
   c) Macvlan. *(Correcta)*
   d) Overlay.

3. **¿Para qué sirve el driver `overlay`?**
   a) Para superponer gráficos en la terminal.
   b) Para conectar contenedores que corren en diferentes nodos (máquinas) de un clúster Docker Swarm. *(Correcta)*
   c) Para ocultar la IP del contenedor.
   d) Para conectar Docker con Kubernetes.

## Preguntas de Desarrollo (30 pts)

4. **Explica la diferencia de aislamiento entre el driver `bridge` y el driver `host`.**
   *Rúbrica*: 10 pts por explicar que `bridge` aísla la red del contenedor en una subred privada y usa NAT/Port Mapping para salir, mientras que `host` elimina el aislamiento de red, haciendo que el contenedor use directamente la interfaz y la pila de red del sistema anfitrión.

5. **Describe un flujo de comunicación típico en una arquitectura de microservicios usando Docker Bridge.**
   *Rúbrica*: 10 pts por describir: Container A (Frontend) -> Red Bridge "AppNet" -> Container B (Backend). Frontend llama a Backend por su nombre de contenedor (ej. `http://backend:3000`), Docker resuelve la IP y enruta el tráfico internamente.

6. **¿Qué sucede si intentas ejecutar dos contenedores con `nginx` usando el driver `host` en la misma máquina?**
   *Rúbrica*: 10 pts por identificar que habrá un conflicto de puertos. Como ambos intentan atarse al puerto 80 de la interfaz del host, el segundo fallará al iniciar porque el puerto ya está en uso.
