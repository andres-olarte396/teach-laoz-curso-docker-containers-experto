# Contenido del Subtema 2 – Services y Networking

## Objetivo
Al finalizar este subtema, serás capaz de:

1.  Comprender por qué las IPs de los Pods no son confiables.
2.  Utilizar el objeto **Service** para ofrecer una IP estable y balanceo de carga.
3.  Diferenciar entre **ClusterIP**, **NodePort** y **LoadBalancer**.

## Contenido Teórico

### 1️⃣ El Problema de la Volatilidad
Los Pods mueren y reviven con nuevas IPs. Si tu Frontend apunta a la IP `10.42.0.5` de tu Backend, y el Backend se reinicia con la IP `10.42.0.8`, tu Frontend se rompe.
Necesitamos una "Dirección Fija" que nunca cambie, independientemente de qué Pods estén vivos.

### 2️⃣ La Solución: Service (SVC)
Un **Service** es una abstracción que define un conjunto lógico de Pods y una política para acceder a ellos.
*   El Service tiene una IP estable (ClusterIP).
*   El Service actúa como un **Load Balancer** interno. Distribuye el tráfico entre todos los Pods que coincidan con su `selector`.

### 3️⃣ Tipos de Servicios
1.  **ClusterIP** (Default): Solo accesible *desde dentro* del clúster. Ideal para bases de datos o backends internos.
2.  **NodePort**: Abre un puerto estático (ej. 30007) en *todos* los nodos del clúster. Permite acceso externo básico (`IP_NODO:PUERTO`).
3.  **LoadBalancer**: Pide a tu proveedor de nube (AWS, Azure, GCP) un Balanceador de Carga real con IP pública. (En local, Docker Desktop simula esto en `localhost`).

### 4️⃣ Manifiesto de un Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mi-servicio
spec:
  selector:
    app: nginx-demo       # ¡Apunta a los Pods con esta etiqueta!
  ports:
  - protocol: TCP
    port: 80              # Puerto del Servicio
    targetPort: 80        # Puerto del Pod
  type: LoadBalancer      # Tipo de exposición
```

## Paso a Paso práctico
1.  Tener un Deployment corriendo (ej. `nginx-deployment`).
2.  Crear `service.yaml`.
3.  Aplicar: `kubectl apply -f service.yaml`.
4.  Verificar IP externa: `kubectl get svc`.
5.  Acceder desde el navegador.

## Resumen
*   **Pods**: IPs efímeras.
*   **Services**: IPs estables y DNS interno (`http://mi-servicio`).
*   **Selector**: El pegamento que une al Service con sus Pods.
