# Ejercicios – Instrucciones Clave

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Tu primer Dockerfile**
1. Crea un directorio vacío.
2. Crea un archivo `index.html` con un "Hola Mundo".
3. Escribe un `Dockerfile` que use `nginx:alpine`, copie el `index.html` a `/usr/share/nginx/html/` y exponga el puerto 80.
4. Construye la imagen (`docker build -t mi-nginx .`) y ejecútala mapeando el puerto 8080 (`docker run -p 8080:80 mi-nginx`).

**Ejercicio 2 – WORKDIR**
1. Modifica el Dockerfile anterior para usar `WORKDIR /usr/share/nginx/html` antes del `COPY`.
2. Cambia la instrucción `COPY` para que sea simplemente `COPY . .`.
3. Reconstruye y verifica que funciona igual.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Variables de Entorno (ENV)**
1. Crea un script en Python `app.py`:
   ```python
   import os
   print(f"Hola {os.environ.get('NAME', 'Desconocido')}")
   ```
2. Crea un Dockerfile basado en `python:3.9-alpine`:
   - Define `ENV NAME=Estudiante`.
   - Copia el script y ejecútalo con `CMD`.
3. Construye y corre la imagen. Debería imprimir "Hola Estudiante".
4. Corre la imagen sobrescribiendo la variable: `docker run -e NAME=Experto mi-python`.

**Ejercicio 4 – COPY vs ADD**
1. Crea un archivo `texto.tar.gz` que contenga un `leeme.txt`.
2. Usa `ADD texto.tar.gz /datos/` en tu Dockerfile.
3. Construye la imagen y explora el contenido (`docker run --rm mi-imagen ls -l /datos`). ¿Se descomprimió automáticamente?

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – CMD vs ENTRYPOINT**
1. Crea un Dockerfile con:
   ```Dockerfile
   FROM alpine
   ENTRYPOINT ["ping"]
   CMD ["google.com"]
   ```
2. Construye como `mi-ping`.
3. Ejecuta `docker run mi-ping` (debería pingear google.com).
4. Ejecuta `docker run mi-ping 1.1.1.1` (debería pingear 1.1.1.1).
5. Explica cómo Docker combinó el ENTRYPOINT con el CMD o el argumento.

**Ejercicio 6 – Usuario no-root (Intro)**
1. Añade `RUN addgroup -S appgroup && adduser -S appuser -G appgroup` a tu Dockerfile (alpine).
2. Usa `USER appuser` al final del Dockerfile.
3. Verifica con `docker run --rm mi-imagen id` que no eres root.
