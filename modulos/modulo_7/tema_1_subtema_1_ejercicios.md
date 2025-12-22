# Ejercicios – Pods y Nodos

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Explorando el Clúster**
1.  Verifica que tu contexto de `kubectl` apunta al lugar correcto (Docker Desktop o Minikube): `kubectl config current-context`.
2.  Lista tus nodos: `kubectl get nodes -o wide`.
    *   ¿Cuántos ves? (En Docker Desktop suele ser 1, `docker-desktop`).
    *   ¿Cuál es su versión de Kernel y OS Image?

**Ejercicio 2 – Tu primer Pod Imperativo**
1.  Crea un pod llamado `mi-primer-pod` usando la imagen `nginx`:
    ```bash
    kubectl run mi-primer-pod --image=nginx
    ```
2.  Verifica que está `Running`: `kubectl get pods`.
3.  Obtén su IP interna: `kubectl get pod mi-primer-pod -o wide`.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Disección con `describe`**
1.  Algo salió mal (simulado). Intenta correr una imagen que no existe:
    ```bash
    kubectl run error-pod --image=nginx:versione-inexistente
    ```
2.  Verifica el estado con `kubectl get pods`. Verás `ErrImagePull` o `ImagePullBackOff`.
3.  Investiga la causa raíz:
    ```bash
    kubectl describe pod error-pod
    ```
4.  Baja hasta la sección "Events". ¿Qué mensaje ves? Esta es la técnica #1 de debugging en K8s.
5.  Borra el pod fallido: `kubectl delete pod error-pod`.

**Ejercicio 4 – Ejecutando comandos dentro del Pod**
1.  Entra en la terminal de `mi-primer-pod`:
    ```bash
    kubectl exec -it mi-primer-pod -- sh
    ```
2.  Ejecuta `hostname`. ¿Coincide el nombre con el del Pod?
3.  Ejecuta `cat /etc/os-release`. ¿Es el SO del nodo o del contenedor? (Spoiler: Contenedor).
4.  Sal con `exit`.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Multi-Container Pod (Dry Run)**
1.  Crear pods multicontenedor imperativamente es difícil. Usaremos la generación de YAML (Dry Run).
2.  Genera el YAML base:
    ```bash
    kubectl run multi-pod --image=nginx --dry-run=client -o yaml > multi.yaml
    ```
3.  Edita `multi.yaml` manualmente. En la sección `containers`, agrega un segundo contenedor (ej. `alpine` que haga un `sleep 3600`).
4.  Aplica el archivo: `kubectl apply -f multi.yaml`.
5.  Verifica con `kubectl get pods`. Debería decir `READY 2/2`.

**Ejercicio 6 – Port Forwarding (Acceso rápido)**
1.  Como los Pods tienen IPs privadas, no puedes acceder a ellos fácilmente desde tu navegador (salvo que configures Services, que veremos luego).
2.  Para pruebas rápidas, usa port-forwarding:
    ```bash
    kubectl port-forward mi-primer-pod 8080:80
    ```
3.  Abre `http://localhost:8080`. ¡Verás Nginx!
4.  Cancela con `Ctrl+C`.
