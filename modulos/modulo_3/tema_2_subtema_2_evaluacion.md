# Evaluación – Backups y Migración

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es la forma recomendada ("Docker way") de hacer backup de un volumen llamado `data_vol`?**
   a) Copiar manualmente la carpeta `/var/lib/docker/volumes/data_vol` como root.
   b) Usar un contenedor temporal que monte `data_vol` y haga un `tar` hacia un directorio del host. *(Correcta)*
   c) Usar `docker commit` para guardar los datos en una nueva imagen.
   d) Hacer una captura de pantalla del contenedor.

2. **Para migrar un volumen de un Host A a un Host B, los pasos lógicos son:**
   a) Backup en A -> Copiar archivo a B -> Restaurar en B. *(Correcta)*
   b) Conectar los dos hosts con un cable USB.
   c) Copiar el ID del volumen de A y pegarlo en B.
   d) Usar `docker push` del volumen.

3. **¿Por qué es arriesgado hacer un backup de archivos de base de datos (ej. copiando la carpeta de datos) mientras el contenedor de la DB está corriendo activamente?**
   a) Porque Docker bloquea la lectura de archivos.
   b) Porque los datos pueden estar inconsistentes o corruptos si hay escrituras en vuelo (memoria no flusheada a disco). *(Correcta)*
   c) Porque el archivo resultante pesará el doble.
   d) No hay riesgo, Docker maneja eso.

## Preguntas de Desarrollo (30 pts)

4. **Escribe el comando (o la estructura del comando) para restaurar un archivo `backup.tar` ubicado en `$(pwd)` hacia un volumen llamado `restore_vol`.**
   *Rúbrica*: 10 pts por una estructura similar a:
   `docker run --rm -v restore_vol:/dest -v $(pwd):/src alpine tar xf /src/backup.tar -C /dest`

5. **Explica por qué usar `docker commit` NO es una estrategia válida para hacer backup de datos persistentes (volúmenes).**
   *Rúbrica*: 10 pts por explicar que `docker commit` guarda los cambios en el sistema de archivos del contenedor (la capa de escritura), pero **ignora** el contenido de los volúmenes montados. Los datos del volumen no se incluirían en la imagen.

6. **Si tienes que hacer un backup de una base de datos crítica en producción sin detener el servicio, ¿qué alternativa es mejor que copiar los archivos del volumen?**
   *Rúbrica*: 10 pts por sugerir el uso de herramientas de volcado lógico (`mysqldump`, `pg_dump`) ejecutadas vía `docker exec`, las cuales garantizan consistencia transaccional sin necesidad de apagar el contenedor.
