# Evaluación – Services y Networking

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es la función principal de un Service en Kubernetes?**
   a) Crear contenedores.
   b) Proveer una IP estable y balanceo de carga para un conjunto de Pods dinámicos. *(Correcta)*
   c) Almacenar datos persistentes.
   d) Gestionar los certificados SSL.

2. **¿Qué tipo de Service es el predeterminado y solo permite acceso desde dentro del clúster?**
   a) NodePort
   b) LoadBalancer
   c) ClusterIP *(Correcta)*
   d) ExternalName

3. **¿Cómo sabe un Service a qué Pods debe enviar el tráfico?**
   a) Por el nombre del Pod.
   b) Utilizando un `selector` que coincide con las `labels` de los Pods. *(Correcta)*
   c) Se debe configurar manualmente cada IP.
   d) Envía tráfico a todos los Pods del nodo.

## Preguntas de Desarrollo (30 pts)

4. **Explica la diferencia entre `port`, `targetPort` y `nodePort` en la definición de un Service.**
   *Rúbrica*: 10 pts por explicar:
   *   `port`: El puerto en el que el Service escucha (IP virtual).
   *   `targetPort`: El puerto en el contenedor (Pod) al que se reenvía el tráfico.
   *   `nodePort`: El puerto estático abierto en cada Nodo físico (solo en tipo NodePort/LoadBalancer).

5. **Si tienes una aplicación web pública, ¿qué tipo de Service usarías normalmente en un proveedor de nube (AWS/GCP) y por qué?**
   *Rúbrica*: 10 pts por elegir **LoadBalancer**, ya que aprovisiona una IP pública externa y gestiona el enrutamiento desde internet hacia los nodos del clúster automáticamente.

6. **Describe qué sucede si el `selector` de un Service no coincide con ninguna etiqueta de tus Pods.**
   *Rúbrica*: 10 pts por explicar que el Service se creará correctamente, pero su lista de `Endpoints` estará vacía. Cualquier tráfico enviado a la IP del Service será rechazado o caerá en "agujero negro" porque no hay Pods destino identificados.
