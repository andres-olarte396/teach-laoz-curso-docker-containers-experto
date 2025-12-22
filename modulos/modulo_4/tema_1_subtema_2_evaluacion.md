# Evaluación – Dependencias y Healthchecks

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué garantiza la instrucción estándar `depends_on: [db]` en Docker Compose?**
   a) Que el servicio actual esperará a que la base de datos acepte conexiones TCP.
   b) Que el servicio `db` se iniciará (estado Running) antes que el servicio actual. *(Correcta)*
   c) Que ambos servicios comparten la misma red.
   d) Que si `db` falla, el servicio actual se reinicia.

2. **¿Cuál es la función principal de un `HEALTHCHECK` en Docker?**
   a) Reparar archivos corruptos automáticamente.
   b) Ejecutar un comando periódicamente para verificar que la aplicación dentro del contenedor funciona correctamente. *(Correcta)*
   c) Escanear virus en la imagen.
   d) Medir el uso de CPU.

3. **¿Qué condición debes añadir a `depends_on` para esperar a un healthcheck exitoso?**
   a) `condition: service_started`
   b) `condition: service_healthy` *(Correcta)*
   c) `wait_for: health`
   d) `status: ok`

## Preguntas de Desarrollo (30 pts)

4. **Explica con un ejemplo por qué `depends_on` sin condiciones no evita errores de conexión con bases de datos pesadas (como Oracle o Postgres).**
   *Rúbrica*: 10 pts por explicar que el proceso del contenedor puede estar "corriendo" (PID activo) mientras la base de datos aún está inicializando ficheros, cargando tablas o escuchando en el socket. La app cliente intentará conectar antes de que el socket esté abierto, fallando.

5. **Escribe un bloque YAML de ejemplo para un healthcheck de un servidor web que corre en el puerto 80.**
   *Rúbrica*: 10 pts por algo similar a:
   ```yaml
   healthcheck:
     test: ["CMD", "curl", "-f", "http://localhost"]
     interval: 30s
     timeout: 10s
     retries: 3
   ```

6. **¿Qué es el `start_period` en la configuración de un Healthcheck y para qué sirve?**
   *Rúbrica*: 10 pts por explicar que es un tiempo de gracia al inicio del contenedor donde los fallos del healthcheck no cuentan para el límite de reintentos (`retries`). Útil para aplicaciones que tardan mucho en arrancar (como Java/Spring) para evitar que se marquen como `unhealthy` prematuramente.
