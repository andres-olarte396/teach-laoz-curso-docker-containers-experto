# Guión de Audio – Logging Drivers

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Pragmático y previsor
- **Audiencia**: Devs que alguna vez han llenado el disco /var a medianoche

## INTRO (30 s)
Los logs son como un diario personal de tu aplicación. Pero imagina que escribes en ese diario cada segundo y nunca cambias de cuaderno. Eventualmente, tu casa se llenaría de papel hasta el techo. Eso es exactamente lo que hace el driver por defecto de Docker si no lo configuras.

## DESARROLLO (2 min)

### 1️⃣ El Peligro de `json-file`
- Docker guarda todo lo que sale por pantalla en un archivo JSON.
- Sin límites, este archivo crece infinitamente. He visto servidores de producción caerse simplemente porque un contenedor escribió 500GB de logs en una semana.
- La solución es obligatoria: **Log Rotation**. `max-size` y `max-file`. Hazlo global en el `daemon.json` y olvídate del problema.

### 2️⃣ Más allá del archivo local
- En entornos serios, no quieres entrar servidor por servidor a leer logs.
- Docker soporta drivers para enviar esos logs a otro lado: `syslog`, `awslogs` para CloudWatch, etc.
- Esto centraliza tu información y la hace buscable.

### 3️⃣ La Trampa de `docker logs`
- Una advertencia: El comando `docker logs` que tanto amas lee del archivo local.
- Si cambias el driver a `syslog` o `splunk`, `docker logs` deja de funcionar, porque Docker ya no guarda copia local.
- Para tener lo mejor de ambos mundos, suele ser mejor usar el driver local (rotado) y tener un agente como Filebeat enviando los logs a la nube.

## CIERRE (30 s)
No dejes que el log sea la causa de muerte de tu servidor. Configura la rotación hoy mismo. Es una línea de configuración que te ahorrará desvelos. ¡A configurar esos drivers!

## NOTAS DE PRODUCCIÓN
- Enfatizar la anécdota de los "500GB de logs".
- Aclarar bien la "Trampa de docker logs" para evitar frustraciones.
