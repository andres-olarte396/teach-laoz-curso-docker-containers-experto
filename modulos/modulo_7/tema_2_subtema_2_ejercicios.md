# Ejercicios – Services y Networking

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Exponer un Deployment (Imperativo)**
1.  Si no tienes el deployment de Nginx, créalo rápidamente:
    `kubectl create deployment nginx-web --image=nginx --replicas=3`
2.  Exponlo con un servicio tipo NodePort:
    `kubectl expose deployment nginx-web --type=NodePort --port=80`
3.  Verifica el puerto asignado: `kubectl get svc nginx-web`. (Busca algo como `80:31543/TCP`).
4.  Si usas Docker Desktop, ve a `http://localhost:31543`.

**Ejercicio 2 – Service Discovery (DNS)**
1.  Crea un pod temporal para probar la red:
    `kubectl run digger --image=alpine -- sleep 3600`
2.  Entra en él: `kubectl exec -it digger -- sh`.
3.  Instala herramientas de red (Alpine): `apk add curl BIND-tools`.
4.  Haz ping al nombre del servicio: `ping nginx-web`.
    *   Verás que resuelve a una IP interna (ClusterIP). ¡Magia del DNS de K8s!
5.  Sal con `exit` y chao `digger`.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – LoadBalancer Declarativo**
1.  Crea un archivo `lb-service.yaml`:
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: public-web
    spec:
      selector:
        app: nginx-web # Asegúrate que coincida con el label de tu deployment
      ports:
        - port: 8080
          targetPort: 80
      type: LoadBalancer
    ```
2.  Aplica: `kubectl apply -f lb-service.yaml`.
3.  Verifica: `kubectl get svc public-web`.
    *   En "EXTERNAL-IP", espera un momento. Debería aparecer `localhost` (Docker Desktop) o una IP real (Cloud).
4.  Abre `http://localhost:8080`.

**Ejercicio 4 – El Selector Roto (Debugging)**
1.  Edita `lb-service.yaml` y cambia el selector a `app: no-existe`.
2.  Aplica los cambios.
3.  Intenta acceder a `http://localhost:8080`. Fallará.
4.  Debuggea: `kubectl describe svc public-web`.
5.  Mira la línea "Endpoints". ¿Está vacía? Si es así, el selector no encuentra pods.
6.  Arréglalo volviendo al selector correcto (`app: nginx-web`).

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Multi-Port Service**
1.  Crea un servicio que exponga dos puertos a la vez (ej. 80 para HTTP y 443 para HTTPS).
2.  Modifica tu YAML para incluir una lista en `ports`.
    ```yaml
    ports:
    - name: http
      port: 80
      targetPort: 80
    - name: https
      port: 443
      targetPort: 80 # Redirigimos todo al 80 por simplicidad en este lab
    ```
3.  Aplica y verifica con `kubectl describe svc`.

**Ejercicio 6 – Limpieza Final**
1.  ¡El curso ha terminado! Limpia tu clúster.
    `kubectl delete all --all`
    (Cuidado: Esto borra TODO en el namespace default. Úsalo solo en entornos de práctica).
