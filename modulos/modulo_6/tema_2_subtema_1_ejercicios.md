# Ejercicios – Intro a Kubernetes

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Hola Kubectl**
1. Asegúrate de tener K8s activo (Docker Desktop, Minikube o Kind).
2. Ejecuta `kubectl version --client`.
3. Ejecuta `kubectl cluster-info` para ver dónde está corriendo tu Control Plane.

**Ejercicio 2 – Tu primer Pod**
1. Diferente a Docker, aquí usamos `create` o `run`.
   `kubectl run demo-nginx --image=nginx:alpine`
2. Estado: `kubectl get pods`.
3. Logs: `kubectl logs demo-nginx`.
4. Borrar: `kubectl delete pod demo-nginx`.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Tu primer Deployment (Imperativo)**
1. En lugar de un pod suelto, crea un deployment escalable:
   `kubectl create deployment web --image=httpd:alpine --replicas=3`
2. Verifica: `kubectl get deployments` y `kubectl get pods`. Deberías ver 3 pods con nombres aleatorios.
3. Escala: `kubectl scale deployment web --replicas=5`.

**Ejercicio 4 – Exponiendo el Servicio**
1. Los pods tienen IPs internas inalcanzables. Crea un servicio para exponerlo:
   `kubectl expose deployment web --type=NodePort --port=80`
2. Busca el puerto asignado: `kubectl get service web`. (Verás algo como `80:31234`).
3. Accede a `http://localhost:31234` (o la IP de tu nodo).

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – YAML Declarativo**
1. Kubernetes brilla con archivos YAML. Genera uno sin ejecutarlo:
   `kubectl create deployment microservicio --image=python:alpine --dry-run=client -o yaml > deploy.yaml`
2. Edita `deploy.yaml` para agregar una variable de entorno `ENV: PROD`.
3. Aplícalo: `kubectl apply -f deploy.yaml`.
4. Esta es la forma profesional de trabajar (GitOps).

**Ejercicio 6 – Auto-healing**
1. Observa los pods del deployment `web`.
2. Borra uno manualmente: `kubectl delete pod <nombre-de-un-pod>`.
3. Inmediatamente ejecuta `kubectl get pods`.
4. Verás que K8s creó uno nuevo para mantener las 5 réplicas que pediste. (Igual que Swarm, pero con Pods).
