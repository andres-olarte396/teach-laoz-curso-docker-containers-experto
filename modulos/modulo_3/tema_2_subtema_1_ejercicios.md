# Ejercicios – Tipos de Monturas

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Persistencia con Volúmenes**
1. Crea un volumen llamado `notas_vol`: `docker volume create notas_vol`.
2. Inicia un contenedor `alpine` montando ese volumen en `/datos`.
3. Crea un archivo dentro: `echo "No me olvides" > /datos/nota.txt`.
4. Elimina el contenedor (`docker rm -f ...`).
5. Inicia un *nuevo* contenedor montando el mismo volumen.
6. Lee el archivo `/datos/nota.txt`. ¿Sigue ahí?

**Ejercicio 2 – Desarrollo con Bind Mounts**
1. Crea una carpeta `sitio-web` y dentro un `index.html` que diga `<h1>Hola Bind Mount</h1>`.
2. Ejecuta un servidor `nginx` mapeando esa carpeta a `/usr/share/nginx/html`.
   *(Pista: usa ruta absoluta o `$(pwd)` en Linux/Powershell)*.
3. Abre el navegador en localhost.
4. Sin detener el contenedor, edita el `index.html` en tu host para decir `<h1>Hola Mundo Editado</h1>`.
5. Refresca el navegador. ¿Cambió instantáneamente?

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Sintaxis `--mount`**
1. Repite el Ejercicio 1 pero usando exclusivamente la sintaxis `--mount type=volume,...`.
2. Repite el Ejercicio 2 usando `--mount type=bind,...`.
3. ¿Qué error da Docker si intentas hacer un bind mount de una carpeta que no existe en el host usando `--mount`? (A diferencia de `-v`, que a veces la crea automáticamente como carpeta vacía).

**Ejercicio 4 – tmpfs para seguridad**
1. Ejecuta un contenedor con una montura tmpfs en `/app/secretos`.
2. Entra con `docker exec` y escribe una contraseña en un archivo dentro de `/app/secretos`.
3. Sal y reinicia el contenedor (`docker restart`).
4. Entra de nuevo y busca el archivo. Explica qué pasó.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Inspect de Monturas**
1. Crea un contenedor con un volumen y un bind mount simultáneos.
2. Ejecuta `docker inspect <container_id>`.
3. Busca la sección `"Mounts"`.
4. Identifica:
   - `Source` (Ruta física en el host).
   - `Destination` (Ruta dentro del contenedor).
   - `RW` (Read/Write status).
5. ¿Dónde guarda Docker realmente los datos de tu volumen `notas_vol`? (Pista: está en el Source del inspect).

**Ejercicio 6 – Read Only Bind Mount**
1. Tienes un archivo de configuración que el contenedor debe leer pero **no debe poder modificar**.
2. Monta ese archivo usando la opción `readonly` (o `ro` en `-v`).
3. Intenta entrar al contenedor y editar el archivo (ej. `echo "cambio" >> /ruta/config`). ¿Qué pasa?
