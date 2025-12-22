# Ejercicios – Seguridad del Docker Daemon

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – El poder del Socket**
1. Lanza un contenedor `alpine` interactivo montando el socket de Docker:
   `docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock docker:cli sh`
   *(Nota: necesitas la imagen que tenga el cliente docker, o instala docker en alpine)*.
2. Dentro del contenedor, ejecuta `docker ps`. Verás los contenedores del host.
3. ¡Peligro! Ejecuta `docker run --rm -v /:/host alpine cat /host/etc/shadow`.
   Acabas de leer las contraseñas del host desde un contenedor. Reflexiona sobre esto.

**Ejercicio 2 – Auditoría de `daemon.json`**
1. Verifica si existe `/etc/docker/daemon.json` en tu sistema.
2. Si no existe, créalo con una configuración básica:
   ```json
   {
     "log-driver": "json-file",
     "log-opts": {
       "max-size": "10m",
       "max-file": "3"
     }
   }
   ```
3. Reinicia Docker (`sudo systemctl restart docker`) y verifica que arranca bien.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Live Restore**
1. Agrega `"live-restore": true` a tu `daemon.json`.
2. Lanza un contenedor `nginx`.
3. Reinicia el servicio docker (`systemctl restart docker` o reinicia Docker Desktop).
4. Verifica si el contenedor `nginx` sigue corriendo (no debería haberse reiniciado). Esto reduce el tiempo de inactividad durante parches de seguridad del daemon.

**Ejercicio 4 – No New Privileges**
1. Lanza un contenedor con `--security-opt=no-new-privileges`.
2. Intenta ejecutar un comando `sudo` o un binario con bit SUID dentro (si la imagen lo tiene). Debería fallar al intentar elevar privilegios.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – User Namespaces (Teórico/Simulado)**
1. Investiga qué hace la opción `userns-remap`.
2. Si estás en Linux, intenta activarla. (Nota: Esto puede requerir reinstalar/mover imágenes existentes ya que cambia los permisos en `/var/lib/docker`).
3. Explica cómo esto mitiga el ataque del Ejercicio 1 (leer `/etc/shadow` del host).

**Ejercicio 6 – TLS Remoto (Hard)**
1. Genera certificados con `openssl` (CA, Server, Client).
2. Configura el daemon para escuchar en `0.0.0.0:2376` usando `--tlsverify`.
3. Intenta conectar desde tu cliente local usando las llaves generadas:
   `docker --tlsverify --tlscacert=ca.pem --tlscert=cert.pem --tlskey=key.pem -H=miservidor:2376 ps`.
