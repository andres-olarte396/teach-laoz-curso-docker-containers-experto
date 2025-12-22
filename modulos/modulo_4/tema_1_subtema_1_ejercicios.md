# Ejercicios – Docker Compose YAML

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Traducción de comandos**
Convierte el siguiente comando imperativo en un archivo `docker-compose.yml`:
```bash
docker run -d --name mi-redis -p 6379:6379 -e ALLOW_EMPTY_PASSWORD=yes bitnami/redis:latest
```

**Ejercicio 2 – Hola Mundo en Compose**
1. Crea un `docker-compose.yml` que lance un servicio `web` usando la imagen `httpd:alpine`.
2. Mapea el puerto 80 del host al 80 del contenedor.
3. Levanta el servicio con `docker compose up`.
4. Detenlo con `Ctrl+C` y observa qué pasa.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Stack LAMP Sencillo**
1. Crea un Compose file con dos servicios:
   - `db`: Imagen `mysql:5.7`, contraseña de root `1234`.
   - `admin`: Imagen `phpmyadmin`, dependiendo de `db`, puerto 8080.
2. Levántalo y accede a PhpMyAdmin en el navegador.
3. Loguéate (Servidor: `db`, Usuario: `root`).
4. Usa `docker compose down` para borrar todo.

**Ejercicio 4 – Bind Mounts en Compose**
1. Modifica el ejercicio del servidor web.
2. Agrega una sección `volumes` al servicio para montar una carpeta local `./html` en `/usr/local/apache2/htdocs/`.
3. Crea un `index.html` en `./html` y verifica que se sirve correctamente.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Nombres de Proyectos**
1. Por defecto, Docker Compose usa el nombre de la carpeta como prefijo (ej. `miproyecto_web_1`).
2. Intenta levantar tu proyecto usando un nombre personalizado: `docker compose -p laboratorio up -d`.
3. Verifica los nombres de los contenedores creados.
4. Intenta hacer `docker compose down` sin especificar el nombre del proyecto. ¿Funciona? (Spoiler: No, no encontrará los contenedores).

**Ejercicio 6 – Sobrescritura de Comandos**
1. Usa la imagen `alpine`.
2. En el `docker-compose.yml`, define un `command: ["sleep", "infinity"]` para que no se apague.
3. Levántalo y verifica que está corriendo.
