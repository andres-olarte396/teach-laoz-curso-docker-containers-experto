# Guión de Audio – Development vs Production

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Estratega y organizado
- **Audiencia**: Devs que usan el mismo `yaml` para todo y sufren por ello

## INTRO (30 s)
¿Tienes un archivo `docker-compose.yml` lleno de comentarios que vas activando y desactivando según si estás programando o desplegando? ¡Detente! Hay una forma profesional de manejar esto: la **Composición de Archivos**.

## DESARROLLO (2 min)

### 1️⃣ La Base Común
- Piensa en tu aplicación. Tanto en tu laptop como en el servidor, usas la misma imagen de base de datos y la misma red interna.
- Todo eso va en el `docker-compose.yml` base. Es el denominador común.

### 2️⃣ El Secreto: Override Automático
- Docker Compose es inteligente. Si encuentra un archivo llamado `docker-compose.override.yml`, lo fusiona automáticamente con el base.
- Aquí pones tus juguetes de desarrollador: el volumen para editar código en vivo, los puertos de debug, las variables de entorno inseguras.
- Como es automático, solo escribes `docker compose up` y ¡pum!, entorno de desarrollo listo.

### 3️⃣ Producción Inmutable
- Para producción, creas un tercer archivo: `docker-compose.prod.yml`.
- Aquí activas los reinicios automáticos, quitas los volúmenes de código (usando la imagen compilada) y cierras puertos innecesarios.
- Al desplegar, le dices a Docker explícitamente: "Usa la base Y usa la configuración de prod".

## CIERRE (30 s)
Mantén tus entornos limpios. Base para estructura, Override para desarrollo, Prod para despliegue. Y no olvides probar los **Perfiles** para esas herramientas de debug que solo usas una vez al mes.

## NOTAS DE PRODUCCIÓN
- Tono enfático en "¡Detente!".
- Explicar "Override" como "sobrescribir" o "modificación".
