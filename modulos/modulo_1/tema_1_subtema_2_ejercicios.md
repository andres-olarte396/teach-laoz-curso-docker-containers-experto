# Ejercicios – Arquitectura Docker Engine

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Componentes**
Describe brevemente cada uno de los siguientes componentes del Docker Engine y su función:
- Docker Daemon (`dockerd`)
- Docker Client (`docker`)
- Docker Registry

**Ejercicio 2 – Flujo de comandos**
Ordena los pasos siguientes tal como ocurren cuando ejecutas `docker run nginx`:
1. El cliente envía la solicitud al daemon.
2. El daemon descarga la imagen del registry (si no está local).
3. El daemon crea un contenedor a partir de la imagen.
4. El contenedor se inicia y expone sus puertos.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Simulación de un build**
Imagina que tienes el siguiente Dockerfile:
```Dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
CMD ["node","server.js"]
```
Describe qué hace cada instrucción y cuál es la capa resultante en la imagen final.

**Ejercicio 4 – Registro privado**
Enumera tres ventajas de usar un registro Docker privado frente a Docker Hub público.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Arquitectura distribuida**
Explica cómo se comunican varios daemons Docker en un clúster Swarm cuando se despliega un servicio con réplicas. Señala el papel del **manager node** y los **worker nodes**.

**Ejercicio 6 – Seguridad del daemon**
Propón dos medidas para proteger el socket Unix `/var/run/docker.sock` y evitar que usuarios no autorizados ejecuten comandos Docker.
