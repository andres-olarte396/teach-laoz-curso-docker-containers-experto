# Ejercicios – Backups y Migración

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Backup manual**
1. Crea un volumen `datos_importantes` e inicia un contenedor que cree un archivo dentro:
   `docker run --rm -v datos_importantes:/data alpine sh -c "echo 'Info vital' > /data/secreto.txt"`
2. Ejecuta el comando mágico para hacer un backup `backup.tar.gz` en tu directorio actual.
3. Verifica que el archivo `.tar.gz` existe en tu host y tiene un tamaño > 0.

**Ejercicio 2 – Restauración**
1. Elimina el volumen original: `docker volume rm datos_importantes`.
2. Crea un nuevo volumen `datos_recuperados`.
3. Restaura el backup en este nuevo volumen.
4. Verifica el contenido:
   `docker run --rm -v datos_recuperados:/data alpine cat /data/secreto.txt`
   ¿Dice "Info vital"?

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Migración simulada**
1. Simula que mueves datos a "otro servidor" (otra carpeta en tu máquina).
2. Mueve el `backup.tar.gz` a una carpeta `/tmp/migracion`.
3. Desde esa carpeta, restaura el backup en un tercer volumen llamado `datos_migrados`.
4. Levanta un servicio (ej. nginx) que use ese volumen y verifica que arranca sin errores.

**Ejercicio 4 – Backup de base de datos en caliente**
(Avanzado conceptual)
Intentar hacer `tar` de los archivos de una DB corriendo puede corromperlos.
Investiga: ¿Qué comando específico de la base de datos (ej. `pg_dump` para Postgres o `mysqldump` para MySQL) deberías ejecutar DESDE DENTRO del contenedor antes de hacer el tar, o en lugar del tar?

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Script de Backup Automático**
1. Escribe un script de shell (`backup.sh`) que:
   - Tome el nombre de un volumen como argumento.
   - Cree un backup con el nombre formatado: `backup_NOMBREVOLUMEN_FECHA.tar.gz`.
2. Pruébalo con tus volúmenes existentes.

**Ejercicio 6 – Docker Volume Clone (Alias copy)**
1. Docker no tiene un comando `docker cp` entre volúmenes.
2. Construye un comando "one-liner" que copie el contenido del `volumen_A` al `volumen_B` directamente, sin crear un archivo intermedio en el host.
   (Pista: Usa `alpine` montando ambos volúmenes y ejecutando `cp -av /origen/. /destino/`).
