# Guión de Audio – Dependencias y Healthchecks

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Solucionador y técnico
- **Audiencia**: Devs que sufren de errores de conexión al inicio

## INTRO (30 s)
¿Alguna vez has visto el error "Connection Refused" justo al levantar tu app, pero si reinicias funciona bien? Eso es una condición de carrera. Tu base de datos es lenta y tu app es impaciente. Hoy vamos a enseñarles modales a tus contenedores.

## DESARROLLO (2 min)

### 1️⃣ El Mito de `depends_on`
- Muchos creen que poner `depends_on: - db` es suficiente.
- Error. Eso solo le dice a Docker: "Arranca la base de datos primero".
- Pero Docker considera que "arrancó" en el milisegundo que el proceso existe. La base de datos puede tardar 10 segundos más en cargar sus archivos. Tu app intenta conectar en el segundo 1 y... ¡Boom! Error.

### 2️⃣ La Solución: Healthchecks
- Un **Healthcheck** es como un médico que revisa el pulso del contenedor cada pocos segundos.
- Le configuramos a la base de datos una prueba: "¿Ya respondes al ping?".
- Mientras no responda, el contenedor está en estado `starting`. Cuando responde, pasa a `healthy`.

### 3️⃣ La Sincronización Perfecta
- Ahora volvemos a Compose.
- Cambiamos el `depends_on` simple por la versión larga: `condition: service_healthy`.
- Esto le dice a tu app: "No te despiertes hasta que la base de datos me diga que está sana".
- Resultado: Cero condiciones de carrera. Arranque robusto y predecible.

## CIERRE (30 s)
Configurar healthchecks requiere un par de líneas extra de YAML, pero te ahorra horas de debugging y scripts de espera hacky (`wait-for-it.sh`). ¡Pruébalo en los ejercicios y haz tu arquitectura a prueba de balas!

## NOTAS DE PRODUCCIÓN
- Enfatizar "¡Boom! Error" para dramatizar el fallo común.
- Explicar `wait-for-it.sh` como algo "vieja escuela" que ya no necesitamos.
