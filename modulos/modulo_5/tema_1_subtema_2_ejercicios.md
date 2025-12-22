# Ejercicios – Usuario No-Root

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Auditoría de Seguridad**
1. Elige 3 de tus imágenes favoritas (ej. `nginx`, `postgres`, `python`).
2. Ejecuta `docker run --rm <imagen> id`.
3. Anota cuáles corren como `root` por defecto y cuáles usan un usuario específico (ej. `postgres` suele correr como usuario `postgres`).

**Ejercicio 2 – Creación de usuario**
1. Crea un Dockerfile basado en `ubuntu`.
2. Agrega los comandos para crear un usuario llamado `deployer` (hint: `useradd -m deployer`).
3. Define `USER deployer`.
4. Construye y corre: `docker run --rm mi-ubuntu whoami`.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – El problema de los puertos**
1. Crea un Dockerfile con `FROM nginx`.
2. Cambia al usuario `nginx` (que ya existe en la imagen) agregando `USER nginx`.
3. Intenta correrlo mapeando el puerto 80.
4. Observa los logs. Debería haber un error de "Permission denied" al intentar atar el puerto 80.
5. Solución: Modifica la configuración de Nginx para escuchar en 8080 y cambia el `EXPOSE`.

**Ejercicio 4 – Permisos de escritura**
1. Crea un Dockerfile donde crees un directorio `/logs` siendo root.
2. Cambia a `USER appuser`.
3. Intenta escribir en `/logs/app.log` con un `RUN` o `CMD`.
4. Arréglalo asignando `chown appuser:appuser /logs` antes de cambiar de usuario.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Nodos y Node**
1. Las imágenes oficiales de `node` traen un usuario llamado `node` creado pero no activado.
2. Escribe un Dockerfile para una app Express.
3. Asegura que los archivos copiados (`COPY . .`) pertenezcan al usuario `node` usando el flag `--chown=node:node`.
4. Configura `USER node`.
5. Levanta la app y confirma que `node_modules` es accesible.

**Ejercicio 6 – Manipulación de UID/GID**
1. A veces el usuario en el contenedor debe coincidir con tu usuario en el host (ej. UID 1000) para compartir volúmenes sin líos de permisos.
2. Modifica el Dockerfile para aceptar `ARG USER_ID`.
3. Crea el usuario con ese ID específico: `RUN useradd -u ${USER_ID} ...`.
4. Construye pasando tu ID: `docker build --build-arg USER_ID=$(id -u) ...`.
