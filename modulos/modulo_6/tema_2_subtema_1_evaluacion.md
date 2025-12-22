# Evaluación – Intro a Kubernetes

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es la unidad atómica de programación (scheduling) más pequeña en Kubernetes?**
   a) Container
   b) Pod *(Correcta)*
   c) Node
   d) Service

2. **¿Qué herramienta de línea de comandos se utiliza para interactuar con un clúster de Kubernetes?**
   a) `docker`
   b) `k8s-cli`
   c) `kubectl` *(Correcta)*
   d) `kubeadm`

3. **¿Cuál es el equivalente aproximado de un `docker service` (Swarm) en Kubernetes para gestionar réplicas de una aplicación stateless?**
   a) StatefulSet
   b) DaemonSet
   c) Deployment *(Correcta)*
   d) Ingress

## Preguntas de Desarrollo (30 pts)

4. **Explica brevemente la relación entre un Pod y un Contenedor.**
   *Rúbrica*: 10 pts por explicar que un Pod es una abstracción que envuelve a uno o más contenedores. Los contenedores dentro de un mismo Pod comparten almacenamiento (volúmenes) y red (misma IP y localhost), actuando como una unidad lógica cohesiva.

5. **Describe qué hace el comando `kubectl apply -f archivo.yaml`.**
   *Rúbrica*: 10 pts por explicar que envía una configuración declarativa (manifiesto) al clúster. K8s compara el estado deseado en el archivo con el estado actual y realiza los cambios necesarios (crear, actualizar o borrar objetos) para que coincidan.

6. **¿Por qué una empresa podría elegir Docker Swarm sobre Kubernetes para un proyecto pequeño o mediano?**
   *Rúbrica*: 10 pts por mencionar la **simplicidad**. Swarm está integrado en Docker, es más fácil de configurar, requiere menos recursos (overhead) y tiene una curva de aprendizaje mucho menor, lo cual es ideal para equipos pequeños sin necesidades complejas de orquestación.
