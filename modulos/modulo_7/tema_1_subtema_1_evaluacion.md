# Evaluación – Pods y Nodos

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **En la jerarquía de Kubernetes, ¿qué relación es correcta?**
   a) Un Pod contiene varios Nodos.
   b) Un Contenedor contiene varios Pods.
   c) Un Nodo contiene varios Pods, y un Pod contiene uno o más contenedores. *(Correcta)*
   d) Los Nodos y Pods son lo mismo.

2. **¿Qué comando utilizarías para ver información detallada (eventos, estado, configuración) de un Pod que está fallando?**
   a) `kubectl get pod`
   b) `kubectl inspect pod`
   c) `kubectl describe pod` *(Correcta)*
   d) `kubectl logs pod`

3. **¿Cuál de las siguientes afirmaciones sobre la dirección IP de un Pod es verdadera?**
   a) Es estática y nunca cambia.
   b) Es la misma que la IP del Nodo.
   c) Es efímera; si el Pod se recrea, obtiene una nueva IP. *(Correcta)*
   d) Los Pods no tienen dirección IP.

## Preguntas de Desarrollo (30 pts)

4. **Explica por qué Kubernetes utiliza el concepto de "Pod" en lugar de manejar contenedores directamente.**
   *Rúbrica*: 10 pts por mencionar:
   *   Abstracción de red (IP compartida) y almacenamiento (volúmenes compartidos).
   *   Soporte para patrones multi-contenedor (ej. sidecars, init-containers) que necesitan trabajar como una unidad cohesiva.
   *   Metadata necesaria para la orquestación (labels, annotations).

5. **Describe el comando para crear un Pod de forma imperativa con la imagen `redis` y exponerlo en el puerto 6379 (aunque el expose no crea el servicio, solo añade metadata).**
   *Rúbrica*: 10 pts por `kubectl run <nombre> --image=redis --port=6379`.

6. **Si tienes un Pod con dos contenedores (App y Sidecar), ¿cómo se comunican entre sí?**
   *Rúbrica*: 10 pts por explicar que comparten el mismo stack de red (Network Namespace), por lo que pueden comunicarse simplemente usando `localhost` y diferentes puertos.
