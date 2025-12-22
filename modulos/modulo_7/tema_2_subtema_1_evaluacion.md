# Evaluación – Deployments y ReplicaSets

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué objeto de Kubernetes es responsable de asegurar que un número específico de réplicas de un Pod esté siempre en ejecución?**
   a) Service
   b) Pod
   c) ReplicaSet (gestionado por un Deployment) *(Correcta)*
   d) Ingress

2. **¿Cuál es la ventaja principal de usar un Deployment en lugar de crear Pods directamente?**
   a) Los Deployments son más rápidos de iniciar.
   b) Permiten actualizaciones controladas (Rolling Updates) y autoreparación (Self-healing). *(Correcta)*
   c) Los Deployments no consumen recursos.
   d) Los Pods directos no soportan volúmenes.

3. **¿Qué sucede durante un Rolling Update predeterminado en un Deployment?**
   a) Se eliminan todos los Pods viejos y luego se crean los nuevos.
   b) Se detiene el clúster.
   c) Se crean Pods nuevos progresivamente y se terminan los viejos solo cuando los nuevos están listos. *(Correcta)*
   d) Se actualiza el código dentro del contenedor sin reiniciarlo.

## Preguntas de Desarrollo (30 pts)

4. **Explica con tus propias palabras el concepto de "Self-Healing" en el contexto de un Deployment.**
   *Rúbrica*: 10 pts por explicar que es la capacidad del controlador de detectar discrepancias entre el estado deseado (ej. 3 réplicas) y el estado actual (ej. 2 réplicas debido a un fallo) y tomar acciones correctivas automáticas (crear una nueva réplica) sin intervención humana.

5. **Describe el proceso para realizar un "Rollback" si una actualización de Deployment falla.**
   *Rúbrica*: 10 pts por mencionar el comando `kubectl rollout undo deployment/<nombre>` (o equivalente) y explicar que esto revierte el estado del Deployment a la revisión estable anterior.

6. **¿Qué es el campo `selector` en un Deployment y por qué es crítico?**
   *Rúbrica*: 10 pts por explicar que el `selector` define qué Pods pertenecen a este Deployment (a través de `matchLabels`). Si los Pods no tienen las etiquetas que el Deployment busca, el ReplicaSet creará nuevos Pods infinitamente pensando que "no tiene ninguno".
