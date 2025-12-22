# Guión de Audio – Variables de Entorno

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Confidencial y práctico
- **Audiencia**: Devs que hardcodean contraseñas (y saben que está mal)

## INTRO (30 s)
Nunca, bajo ninguna circunstancia, escribas contraseñas o claves de API directamente en tu `docker-compose.yml`. Si subes eso a GitHub, has perdido. Hoy aprenderemos a separar la configuración del código usando **Variables de Entorno**.

## DESARROLLO (2 min)

### 1️⃣ El Archivo `.env`
- Es un archivo de texto simple: `CLAVE=VALOR`.
- Docker Compose lo lee automáticamente antes de empezar.
- Puedes usar estas variables para cambiar versiones de imágenes, puertos o configuraciones dinámicas en el propio YAML.
- Ejemplo: `image: postgres:${PG_VERSION}`. Así cambias la versión sin tocar el código.

### 2️⃣ Inyectando al Contenedor
- También necesitas pasar variables *adentro* de la aplicación (como `DB_HOST`).
- Tienes dos opciones elegantes:
  1. **environment**: Para una o dos variables puntuales.
  2. **env_file**: Para cargar 50 variables de golpe desde un archivo. Es mucho más limpio.

### 3️⃣ Regla de Oro: `.env.example`
- Agrega `.env` a tu `.gitignore` inmediatamente.
- Crea un archivo `.env.example` con claves vacías o valores falsos. Ese sí se sube al repo.
- Así, cuando un compañero clone el proyecto, solo tiene que copiar el example y poner sus propios valores.

## CIERRE (30 s)
Las variables de entorno son la base de la metodología "12-Factor App". Hacen que tu app sea portátil y segura. Domina la jerarquía de precedencia en los ejercicios y nunca más tendrás que borrar un commit por revelar secretos.

## NOTAS DE PRODUCCIÓN
- Tono muy serio al hablar de subir secretos a GitHub.
- Explicación clara de "12-Factor App" no necesaria, solo mención como "buenas prácticas estándar".
