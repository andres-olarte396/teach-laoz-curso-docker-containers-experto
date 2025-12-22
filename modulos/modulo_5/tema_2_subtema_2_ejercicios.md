# Ejercicios – Logging Drivers

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Inspección de Logs**
1. Lanza un contenedor `nginx`.
2. Ejecuta `docker inspect --format '{{.HostConfig.LogConfig.Type}}' <container_id>`.
3. Debería decir `json-file` (si no has cambiado la config global).
4. Encuentra la ruta real del log en el disco usando: `docker inspect --format '{{.LogPath}}' <container_id>`.

**Ejercicio 2 – Log Rotation**
1. Lanza un contenedor "spam" que genere logs rápido:
   `docker run -d --name spammer --log-opt max-size=1k --log-opt max-file=2 alpine sh -c "while true; do echo 'llenando disco...'; sleep 0.1; done"`
2. Espera unos segundos.
3. Busca el archivo de log (ver ejercicio 1) y verifica su tamaño (debería ser muy pequeño).
4. Verifica que `docker logs spammer` solo muestra las últimas líneas, confirmando la rotación.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Driver Syslog**
1. Lanza un contenedor usando syslog:
   `docker run -d --name syslogger --log-driver syslog alpine echo "Hola Syslog"`
2. Intenta hacer `docker logs syslogger`. ¿Qué error recibes?
3. Revisa `/var/log/syslog` (o `/var/log/messages` en CentOS/RHEL) en tu host. Deberías ver el mensaje "Hola Syslog".

**Ejercicio 4 – Configuración Global**
1. Edita (o crea) `/etc/docker/daemon.json` para usar el driver `local` con rotación por defecto.
   ```json
   {
     "log-driver": "local",
     "log-opts": {
       "max-size": "5m"
     }
   }
   ```
2. Reinicia Docker.
3. Lanza un nuevo contenedor e inspecciona su driver.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Modos de Entrega (Blocking vs Non-Blocking)**
1. Docker envía logs al driver de forma **síncrona (blocking)** por defecto. Si el driver es lento (ej. red saturada hacia Splunk), la aplicación se congela.
2. Investiga el flag `--log-opt mode=non-blocking`.
3. Lanza un contenedor con driver `syslog` y modo `non-blocking`, con un `max-buffer-size=4m`.
   `docker run --log-driver syslog --log-opt mode=non-blocking --log-opt max-buffer-size=4m alpine echo "Async"`

**Ejercicio 6 – Dual Logging (Teórico)**
1. A veces quieres enviar logs a ELK (remoto) PERO también poder hacer `docker logs` para debugging rápido.
2. Docker nativamente solo soporta un driver a la vez.
3. Investiga cómo lograr esto (Pista: Usar el driver `json-file` y un agente externo como Filebeat instalado en el host que lea los archivos JSON y los envíe a ELK).
