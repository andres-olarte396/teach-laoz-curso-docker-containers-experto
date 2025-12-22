# Evaluación – Usuario No-Root

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es el UID (User ID) por defecto del usuario `root` dentro de un contenedor Linux?**
   a) 1000
   b) 1
   c) 0 *(Correcta)*
   d) -1

2. **¿Qué instrucción de Dockerfile cambia el usuario activo para las siguientes instrucciones?**
   a) `SUDO`
   b) `USER` *(Correcta)*
   c) `LOGIN`
   d) `CHANGE_USER`

3. **¿Por qué suele fallar una aplicación web (ej. Nginx) al ejecutarse como usuario no-root si intenta escuchar en el puerto 80?**
   a) Porque Docker bloquea el puerto 80 por defecto.
   b) Porque en Linux, los puertos privilegiados (< 1024) solo pueden ser abiertos por root. *(Correcta)*
   c) Porque el firewall del contenedor está activo.
   d) No falla, funciona perfectamente.

## Preguntas de Desarrollo (30 pts)

4. **Explica el riesgo de seguridad conocido como "Container Breakout" y cómo correr como no-root ayuda a mitigarlo.**
   *Rúbrica*: 10 pts por explicar que si un atacante explota una vulnerabilidad en la aplicación y logra salir del contenedor al host, si el proceso era root dentro, podría mantener privilegios elevados fuera (dependiendo de la configuración del runtime/kernel), comprometiendo todo el nodo. Al ser no-root, incluso si escapa, tendrá privilegios limitados en el host.

5. **Escribe la línea de un Dockerfile para copiar todo el contenido actual (`.`) al directorio de trabajo, asegurando que el propietario sea el usuario `nodejs` y el grupo `nodejs`.**
   *Rúbrica*: 10 pts por: `COPY --chown=nodejs:nodejs . .`

6. **Si tienes que crear un usuario en una imagen basada en Alpine Linux, ¿qué comando usarías en el RUN?**
   *Rúbrica*: 10 pts por `adduser -S <nombre>` (o variantes válidas de alpine como `adduser -D`). Mencionar `useradd` (de debian/centos) es aceptable si se aclara el contexto, pero la pregunta especifica Alpine.
