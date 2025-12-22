# Guión de Audio – Backups y Migración

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Preventivo y profesional
- **Audiencia**: Ops y Sysadmins responsables de la data

## INTRO (30 s)
Los discos fallan. Los servidores mueren. Los desarrolladores borran cosas por error. Si tus datos solo viven en un volumen Docker sin respaldo, estás jugando a la ruleta rusa. Hoy vamos a asegurar tu activo más valioso: los datos.

## DESARROLLO (2 min)

### 1️⃣ La Técnica del Contenedor Efímero
- Docker no tiene un botón de "Exportar Volumen".
- La técnica estándar es usar un "sidecar": lanzamos un contenedor `alpine` pequeño que monta tu volumen Y una carpeta de tu host.
- Este pequeño ayudante empaqueta todo en un `.tar.gz` y te lo deja en el host. Luego, desaparece (`--rm`). Es limpio y eficiente.

### 2️⃣ Restauración y Migración
- Restaurar es simplemente invertir el proceso.
- Esta técnica hace que la migración sea trivial:
  1. Haces backup en el Servidor Viejo.
  2. Envías el archivo `.tar` por SCP al Servidor Nuevo.
  3. Restauras en el Servidor Nuevo.
- ¡Listo! Tu base de datos o tus archivos han viajado de máquina sin complicaciones.

### 3️⃣ Bases de Datos vs Archivos
- **OJO**: Si respaldas una base de datos (MySQL, Postgres), simplemente copiar los archivos (`/var/lib/mysql`) puede ser riesgoso si la DB está escribiendo en ese momento.
- Para máxima seguridad, usa las herramientas nativas (`mysqldump`, `pg_dump`) a través de `docker exec`, o detén el contenedor de base de datos antes de lanzar el backup.

## CIERRE (30 s)
Un backup no existe hasta que no has probado restaurarlo. No confíes ciegamente en tus scripts. Practica la restauración en los ejercicios de hoy y duerme tranquilo sabiendo que tus volúmenes están a salvo.

## NOTAS DE PRODUCCIÓN
- Tono serio en la advertencia sobre bases de datos.
- Enfatizar "probar restaurarlo".
