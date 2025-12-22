# Evaluación – Docker Compose YAML

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es el nombre por defecto del archivo de configuración que busca el comando `docker compose`?**
   a) `Dockerfile`
   b) `compose.json`
   c) `docker-compose.yml` *(Correcta)*
   d) `stack.yaml`

2. **¿Qué comando se utiliza para detener y eliminar contenedores, redes y (opcionalmente) volúmenes creados por Compose?**
   a) `docker compose stop`
   b) `docker compose down` *(Correcta)*
   c) `docker compose rm`
   d) `docker compose delete`

3. **En un archivo `docker-compose.yml`, ¿bajo qué sección principal se definen los contenedores?**
   a) `containers:`
   b) `pods:`
   c) `services:` *(Correcta)*
   d) `apps:`

## Preguntas de Desarrollo (30 pts)

4. **Traduce el siguiente flag de `docker run` a su equivalente en YAML:**
   `-v /host/data:/container/data`
   *Rúbrica*: 10 pts por escribir:
   ```yaml
   volumes:
     - /host/data:/container/data
   ```

5. **Explica la ventaja de usar una definición "Declarativa" (Compose) frente a una "Imperativa" (CLI).**
   *Rúbrica*: 10 pts por explicar que en el modelo declarativo defines el *estado deseado* final y puedes versionar esa configuración en git, facilitando compartir el entorno exacto con otros desarrolladores, mientras que el imperativo depende de ejecutar comandos manuales propensos a error humano.

6. **¿Qué sucede si ejecutas `docker compose up` dos veces seguidas sin cambiar nada en el YAML?**
   *Rúbrica*: 10 pts por explicar que Docker Compose es **idempotente**. La segunda vez detectará que los contenedores ya están corriendo y coinciden con la configuración, por lo que no hará nada (o simplemente dirá que están "Up-to-date"). No crea duplicados.
