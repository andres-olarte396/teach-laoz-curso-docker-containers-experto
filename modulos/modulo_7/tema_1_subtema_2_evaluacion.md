# Evaluación – Manifiestos YAML

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuáles son los 4 campos de nivel raíz obligatorios en cualquier manifiesto YAML de Kubernetes?**
   a) name, image, port, version
   b) apiVersion, kind, metadata, spec *(Correcta)*
   c) k8s, object, config, status
   d) header, body, footer, auth

2. **¿Qué comando se considera la "navaja suiza" para crear y actualizar recursos de forma declarativa?**
   a) `kubectl create`
   b) `kubectl replace`
   c) `kubectl apply` *(Correcta)*
   d) `kubectl make`

3. **¿Qué ocurre si ejecutas `kubectl apply -f archivo.yaml` sobre un recurso que ya existe y no tiene cambios en el archivo?**
   a) Kubernetes devuelve un error de "ResourceExists".
   b) Kubernetes borra el recurso y lo crea de nuevo.
   c) Kubernetes no realiza ninguna acción (Idempotencia). *(Correcta)*
   d) Se crea un duplicado con otro nombre.

## Preguntas de Desarrollo (30 pts)

4. **Explica la diferencia entre el enfoque imperativo y el declarativo.**
   *Rúbrica*: 10 pts por explicar que en el imperativo indicas los pasos/comandos para crear algo, mientras que en el declarativo describes el estado final deseado y el sistema se encarga de alcanzarlo.

5. **En un archivo YAML, ¿para qué sirve la sección `metadata`?**
   *Rúbrica*: 10 pts por mencionar que contiene información para identificar el objeto, principalmente su `name` (nombre único en el namespace), `namespace` (si aplica) y `labels` (etiquetas para organización y selección).

6. **¿Por qué es una buena práctica guardar los manifiestos YAML en un sistema de control de versiones (como Git)?**
   *Rúbrica*: 10 pts por mencionar:
   *   Historial de cambios (auditoría).
   *   Posibilidad de revertir (rollback) a versiones anteriores.
   *   Colaboración en equipo.
   *   Base para metodologías GitOps.
