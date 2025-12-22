# Ejercicios – Gestión de Caché

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Orden de instrucciones**
1. Tienes el siguiente Dockerfile. Reorganízalo para optimizar la caché:
   ```Dockerfile
   FROM python:3.9
   WORKDIR /app
   COPY . .
   RUN pip install -r requirements.txt
   CMD ["python", "app.py"]
   ```
2. Explica por qué tu versión es mejor.

**Ejercicio 2 – Cache Miss en acción**
1. Crea un Dockerfile con `RUN echo "Paso 1"` y luego `RUN echo "Paso 2"`.
2. Construye la imagen.
3. Modifica el Dockerfile cambiando "Paso 1" a "Paso 1 Modificado".
4. Construye de nuevo y observa los logs. ¿Se ejecutó "Paso 2" de nuevo? ¿Por qué?

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – La trampa de `apt-get`**
1. Crea un Dockerfile con:
   ```Dockerfile
   FROM ubuntu
   RUN apt-get update
   RUN apt-get install -y curl
   ```
2. Construye la imagen.
3. Semanas después, agregas `vim`:
   ```Dockerfile
   FROM ubuntu
   RUN apt-get update
   RUN apt-get install -y curl vim
   ```
4. ¿Por qué esto podría fallar o instalar paquetes viejos? ¿Cómo se arregla agrupando con `&&`?

## Nivel Avanzado (≈ 15 min)

**Ejercicio 4 – Cache Mounts con BuildKit**
1. Asegúrate de tener BuildKit habilitado (viene por defecto en versiones nuevas).
2. Crea un proyecto Node.js.
3. Usa la siguiente instrucción en tu Dockerfile:
   `RUN --mount=type=cache,target=/root/.npm npm install`
4. Borra `node_modules`, cambia una dependencia en `package.json` y reconstruye.
5. Deberías notar que npm descarga solo la nueva librería y reutiliza el resto desde el caché montado, sin volver a bajar todo internet.

**Ejercicio 5 – Invalidación forzada**
1. A veces quieres forzar la invalidación (ej. clonar un repo git que cambió).
2. Usa `ARG CACHEBUST=1` antes del `RUN git clone ...`.
3. Construye con `docker build --build-arg CACHEBUST=$(date +%s) .`.
4. Verifica que siempre clona de nuevo.
