# Ejercicios – Dependencias y Healthchecks

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Orden de arranque básico**
1. Crea un `docker-compose.yml` con dos servicios `alfa` y `beta` (usa imagen `alpine` con un comando `sleep infinity`).
2. Haz que `beta` dependa de `alfa`.
3. Ejecuta `docker compose up -d` y verifica el orden en los eventos (puedes usar `docker compose events`).

**Ejercicio 2 – Creando un Healthcheck manual**
1. Lanza un contenedor Nginx con un healthcheck en línea:
   ```bash
   docker run -d --name salud --health-cmd "curl -f http://localhost || exit 1" --health-interval 5s nginx
   ```
2. Ejecuta `docker ps` y observa la columna "STATUS". Debería decir `(health: starting)` y luego `(healthy)`.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – La espera larga**
1. Crea un `docker-compose.yml`.
2. Servicio 1 (`lento`): Usa `alpine`, simula una inicialización lenta.
   `command: sh -c "sleep 10; echo 'Listo' > /tmp/ready; sleep infinity"`
   Healthcheck: `test: "cat /tmp/ready"`
3. Servicio 2 (`ansioso`): `depends_on` de `lento` con `condition: service_healthy`.
4. Levanta con `docker compose up`. Cronometra cuánto tarda `ansioso` en arrancar.

**Ejercicio 4 – Autorestart por mala salud**
1. Investiga cómo reiniciar un contenedor si se vuelve `unhealthy`.
2. (Pista: No es nativo de Compose v2 directo, se suele usar `autoheal` externo o orquestadores, pero intenta buscar si tu versión soporta reiniciar dependientes).
   *Nota: En Swarm sí es nativo. En Compose local, a veces se requiere un container auxiliar como `willfarrell/autoheal`.*
   Implementa un healthcheck que falle (ej. `exit 1`) y observa qué hace Docker (spoiler: marcarlo unhealthy, pero no reiniciarlo por defecto).

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Healthcheck para Base de Datos**
1. Configura un servicio `mysql` o `mariadb`.
2. Escribe un healthcheck correcto que use `mysqladmin ping -h localhost`.
3. Agrega un servicio `adminer` (interfaz web) que **solo** inicie cuando la base de datos esté lista.
4. Verifica los logs para confirmar la secuencia.

**Ejercicio 6 – Intervalos y Retries**
1. Juega con los valores de `interval`, `timeout`, `start_period` y `retries`.
2. Configura un servicio que tarde 30 segundos en arrancar (Java/Spring Boot simulado con `sleep`) pero que falle si el healthcheck empieza a ejecutarse inmediatamente.
3. Usa `start_period` para dar un tiempo de gracia antes de contar fallos.
