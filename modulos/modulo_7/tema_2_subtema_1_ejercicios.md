# Ejercicios – Deployments y ReplicaSets

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Tu primer Deployment**
1.  Crea un archivo `nginx-deploy.yaml`:
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-deployment
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx:1.23
            ports:
            - containerPort: 80
    ```
2.  Aplica: `kubectl apply -f nginx-deploy.yaml`.
3.  Verifica el estado: `kubectl get deployment nginx-deployment`.

**Ejercicio 2 – Escalado Declarativo**
1.  Edita el archivo `nginx-deploy.yaml`. Cambia `replicas: 2` a `replicas: 5`.
2.  Aplica: `kubectl apply -f nginx-deploy.yaml`.
3.  Observa la magia: `kubectl get pods -w` (usa Ctrl+C para salir del watch).

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Prueba de Resiliencia (Self-healing)**
1.  Lista los pods: `kubectl get pods -l app=nginx`.
2.  Elige uno al azar y bórralo: `kubectl delete pod <nombre-del-pod>`.
3.  Inmediatamente lista los pods de nuevo. Verás que hay un pod nuevo (con edad de pocos segundos) reemplazando al muerto. El Deployment cumplió su promesa de mantener 5 réplicas.

**Ejercicio 4 – Rolling Update**
1.  Vamos a actualizar la versión de Nginx.
2.  Edita `nginx-deploy.yaml`. Cambia `image: nginx:1.23` a `image: nginx:latest`.
3.  Aplica.
4.  Observa el proceso: `kubectl rollout status deployment/nginx-deployment`.
5.  Verás cómo se completó la actualización sin tirar el servicio.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Rollback**
1.  Imagina que la versión `latest` tiene un bug. ¡Volvamos atrás!
2.  Verifica el historial: `kubectl rollout history deployment/nginx-deployment`.
3.  Deshaz el cambio: `kubectl rollout undo deployment/nginx-deployment`.
4.  Verifica que volvió a la versión anterior (describe el deployment para ver la imagen).

**Ejercicio 6 – Escalado Imperativo (Opcional)**
1.  Aunque no es ideal para GitOps, a veces necesitas escalar rápido en una emergencia.
2.  `kubectl scale deployment nginx-deployment --replicas=10`.
3.  Verifica con `kubectl get pods`. (Recuerda que tu archivo YAML ahora está desincronizado con la realidad).
