# Evaluación – Logging Drivers

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es el driver de logging por defecto en Docker y cuál es su comportamiento predeterminado respecto al tamaño?**
   a) `syslog`, rota cada 10MB.
   b) `json-file`, sin límite de tamaño (crece infinitamente). *(Correcta)*
   c) `local`, rota cada 100MB.
   d) `none`, no guarda logs.

2. **Si ejecutas `docker run --log-driver syslog ...`, ¿qué sucederá al ejecutar `docker logs <contenedor>`?**
   a) Verás los logs normalmente.
   b) Verás los logs del host.
   c) Recibirás un error indicando que el driver configurado no soporta lectura de logs. *(Correcta)*
   d) Docker se bloqueará.

3. **¿Qué opción de configuración define el número máximo de archivos de log rotados que se deben conservar?**
   a) `max-size`
   b) `max-file` *(Correcta)*
   c) `log-rotate`
   d) `keep-logs`

## Preguntas de Desarrollo (30 pts)

4. **Explica por qué es una buena práctica configurar la rotación de logs a nivel global en `daemon.json` en lugar de hacerlo contenedor por contenedor.**
   *Rúbrica*: 10 pts por explicar que configurarlo globalmente actúa como una red de seguridad ("safety net") para todos los contenedores, evitando que un desarrollador olvide poner los flags en un despliegue y llene el disco accidentalmente.

5. **Describe el riesgo de usar un driver de logging remoto en modo "blocking" (bloqueante).**
   *Rúbrica*: 10 pts por explicar que en modo blocking, la salida estándar de la aplicación se pausa si el driver de logging no puede confirmar la escritura (ej. si el servidor de logs remoto está caído o lento). Esto efectivamente congela la aplicación, causando una denegación de servicio inducida por el sistema de logs.

6. **Si decides usar ElasticSearch (ELK) para ver tus logs, ¿qué arquitectura recomiendas: A) Driver GELF directo desde Docker, o B) Driver JSON-file + Filebeat? ¿Por qué?**
   *Rúbrica*: 10 pts por argumentar a favor de B (generalmente).
   - A (GELF): Pierdes `docker logs`. Si ELK cae, contenedores pueden bloquearse.
   - B (Filebeat): Mantienes `docker logs` local para diagnósticos urgentes. Filebeat maneja el buffer y reintentos sin afectar al rendimiento del contenedor. La rotación local previene llenado de disco.
