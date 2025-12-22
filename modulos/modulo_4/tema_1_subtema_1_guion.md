# Guión de Audio – Docker Compose YAML

## Metadata
- **Duración estimada**: 4 minutos
- **Tono**: Entusiasta y liberador
- **Audiencia**: Devs cansados de scripts de bash largos

## INTRO (30 s)
¿Harto de escribir comandos `docker run` kilométricos con veinte flags diferentes? ¡Tengo buenas noticias! Hoy conocerás a tu nuevo mejor amigo: **Docker Compose**. La herramienta que transformará tus scripts imperativos en una arquitectura elegante y declarativa.

## DESARROLLO (2 min 30 s)

### 1️⃣ De Imperativo a Declarativo
- Hasta ahora, le decías a Docker qué hacer paso a paso: "Bajame esta imagen", "Luego crea esta red", "Ahora corre este contenedor".
- Con Compose, defines el **resultado final** en un archivo YAML. Dices: "Quiero un sistema con una base de datos y un frontend conectados". Docker se encarga de los pasos intermedios.

### 2️⃣ Estructura del YAML
- El archivo `docker-compose.yml` tiene tres secciones clave:
  1. **services**: Aquí vive tu aplicación. "Web", "Api", "Base de Datos". Cada uno es un contenedor.
  2. **networks**: Las carreteras por donde viajan tus datos.
  3. **volumes**: Tus discos duros virtuales para persistencia.

### 3️⃣ Magia "Up" y "Down"
- Olvídate de recordar si el contenedor se llamaba `web` o `web_v2`.
- `docker compose up -d`: Docker lee el archivo, crea las redes, los volúmenes y levanta los contenedores en el orden correcto.
- `docker compose down`: Destruye todo limpiamente. Es como tener un botón de "Reset" para tu entorno de desarrollo.

## CIERRE (30 s)
Docker Compose es el estándar para desarrollo local. Si tu proyecto tiene más de un contenedor (y casi todos lo tienen), necesitas esto. Empieza a traducir tus comandos `run` a `yaml` en los ejercicios. ¡Tu "yo" del futuro te lo agradecerá!

## NOTAS DE PRODUCCIÓN
- Usar tono de alivio al mencionar `docker compose up`.
- Pronunciar "YAML" como "Yamel".
