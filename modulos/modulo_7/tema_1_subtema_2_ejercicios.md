# Ejercicios – Manifiestos YAML

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Tu primer Manifiesto**
1.  Crea un archivo llamado `pod-manual.yaml` con el siguiente contenido:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: yaml-pod
      labels:
        curso: docker-experto
    spec:
      containers:
      - name: main
        image: redis:alpine
    ```
2.  Aplícalo: `kubectl apply -f pod-manual.yaml`.
3.  Verifica: `kubectl get pod yaml-pod --show-labels`.

**Ejercicio 2 – Generación Automática (Dry Run)**
1.  Escribir YAML desde cero es propenso a errores. Truco pro:
    ```bash
    kubectl run generado --image=nginx --restart=Never --dry-run=client -o yaml > generado.yaml
    ```
2.  Abre `generado.yaml` y estúdialo. K8s genera algunos campos extra por defecto.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Modificación Declarativa**
1.  Edita `pod-manual.yaml`.
2.  Cambia la imagen `redis:alpine` por `redis:7`.
3.  Agrega un nuevo label en metadata: `tier: backend`.
4.  Aplica el cambio: `kubectl apply -f pod-manual.yaml`.
5.  Observa el output. ¿Dice `configured` o `created`? (Debería decir `configured`).
6.  Verifica los cambios: `kubectl describe pod yaml-pod`.

**Ejercicio 4 – Validación de Sintaxis**
1.  Edita `pod-manual.yaml` e introduce un error intencional (ej. cambia `kind: Pod` a `Kind: pod` o rompe la indentación).
2.  Intenta aplicar.
3.  Lee el error de validación. K8s es muy estricto con el YAML.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Multi-Recurso**
1.  En un solo archivo YAML puedes poner varios objetos separados por `---`.
2.  Crea `stack.yaml`:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: app-db
    spec:
      containers:
      - name: db
        image: mongo
    ---
    apiVersion: v1
    kind: Pod
    metadata:
      name: app-web
    spec:
      containers:
      - name: web
        image: nginx
    ```
3.  Aplica: `kubectl apply -f stack.yaml`.
4.  K8s creará ambos objetos en orden.

**Ejercicio 6 – Limpieza Declarativa**
1.  Para borrar lo que creaste con un archivo, no necesitas buscar los nombres.
2.  Ejecuta: `kubectl delete -f stack.yaml`.
3.  K8s leerá el archivo y borrará los recursos definidos en él.
