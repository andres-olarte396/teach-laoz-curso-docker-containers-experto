# Ejercicios – Ciclo de vida básico

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Crear y Detener**
1. Ejecuta un contenedor `nginx` en modo detached (`-d`) llamado `web-test`.
2. Verifica que está corriendo con `docker ps`.
3. Detén el contenedor con `docker stop web-test`.
4. Verifica que ya no aparece en `docker ps`, pero sí en `docker ps -a`.

**Ejercicio 2 – Logs**
1. Inicia nuevamente el contenedor `web-test`.
2. Ejecuta `docker logs web-test` y observa la salida.
3. Intenta acceder a localhost (si expusiste puertos) o simplemente reinicia el contenedor y vuelve a ver los logs para ver las nuevas entradas.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Ejecución de comandos (exec)**
1. Con el contenedor `web-test` corriendo, entra a su shell interactiva: `docker exec -it web-test bash` (o `sh` si bash no está disponible).
2. Dentro del contenedor, crea un archivo: `echo "Hola desde dentro" > /tmp/mensaje.txt`.
3. Sal del contenedor (`exit`) y verifica que el contenedor sigue corriendo.
4. Ejecuta `docker exec web-test cat /tmp/mensaje.txt` desde tu host para leer el archivo.

**Ejercicio 4 – Pausa y Reinicio**
1. Pausa el contenedor `web-test`: `docker pause web-test`.
2. Intenta hacer `docker exec` (debería fallar o quedarse bloqueado).
3. Reanuda el contenedor: `docker unpause web-test`.
4. Reinicia el contenedor: `docker restart web-test`. Verifica el tiempo de actividad (`STATUS`) en `docker ps`.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Limpieza (Prune y RM)**
1. Crea un contenedor que termine inmediatamente: `docker run --name efimero busybox echo "Adios"`.
2. Verifica su estado con `docker ps -a` (debe ser `Exited`).
3. Elimínalo manualmente: `docker rm efimero`.
4. Crea tres contenedores "basura" detenidos.
5. Usa `docker container prune` para eliminarlos todos de una vez y observa el espacio reclamado.

**Ejercicio 6 – Modo Interactivo vs Detached**
1. Ejecuta `docker run -it --name interactivo ubuntu bash`. Juega en la terminal y luego escribe `exit`.
2. Comprueba que el contenedor se detuvo.
3. Ejecuta `docker start -ai interactivo` para volver a entrar a la misma sesión.
4. Explica la diferencia entre este flujo y `docker run -d`.
