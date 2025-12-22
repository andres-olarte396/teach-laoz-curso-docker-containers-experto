# Ejercicios – Variables de Entorno

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Sustitución Básica**
1. Crea un archivo `.env` con `VERSION=3.9`.
2. Crea un `docker-compose.yml`:
   ```yaml
   services:
     py:
       image: python:${VERSION}-alpine
       command: python --version
   ```
3. Ejecuta `docker compose up`. ¿Qué versión imprime?
4. Cambia `.env` a `VERSION=3.8` y repite. ¿Cambió la imagen descargada?

**Ejercicio 2 – Passthrough**
1. En tu terminal (PowerShell o Bash), exporta una variable: `export SECRETO=1234` (o `$env:SECRETO="1234"`).
2. Crea un compose file:
   ```yaml
   services:
     test:
       image: alpine
       command: env
       environment:
         - SECRETO
   ```
3. Ejecuta `docker compose up`. Busca `SECRETO` en la salida.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – `env_file` vs `environment`**
1. Crea `archivo.env` con `TIPO=Archivo`.
2. En `docker-compose.yml`, usa `env_file: [archivo.env]` Y TAMBIÉN `environment: ["TIPO=Manual"]`.
3. Levanta un contenedor que imprima la variable `TIPO`.
4. ¿Cuál ganó? (Verifica la jerarquía de precedencia).

**Ejercicio 4 – Valores por defecto**
1. Modifica el ejercicio 1 para usar una sintaxis de valor por defecto en el YAML: `${VERSION:-latest}`.
2. Borra o renombra tu archivo `.env`.
3. Ejecuta `docker compose config`. ¿Qué imagen muestra ahora?

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Escapando variables**
1. Intenta usar una variable que contenga el signo `$` literalmente (ej. una contraseña tipo `pass$word`).
2. Investiga cómo escapar el signo `$` en `docker-compose.yml` para que Compose no intente interpolarlo. (Pista: `$$`).

**Ejercicio 6 – .env múltiple**
1. Crea `.env` y `.env.prod`.
2. Investiga cómo decirle a docker compose que use `.env.prod` en lugar del predeterminado. (Pista: flag `--env-file`).
