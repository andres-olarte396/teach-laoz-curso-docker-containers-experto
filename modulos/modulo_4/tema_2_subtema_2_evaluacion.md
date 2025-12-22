# Evaluación – Variables de Entorno

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué archivo busca Docker Compose automáticamente en el directorio actual para cargar variables?**
   a) `config.json`
   b) `.env` *(Correcta)*
   c) `variables.yaml`
   d) `docker.conf`

2. **Si defines una variable en `.env` y la misma variable en la sección `environment` del `docker-compose.yml`, ¿cuál valor verá el proceso dentro del contenedor?**
   a) El de `.env`.
   b) El de `environment`. *(Correcta: environment sobrescribe .env si se pasa explícitamente)*
   c) Ambos concatenados.
   d) Docker da error.

3. **¿Cuál es la sintaxis correcta para pasar una variable de entorno desde el host al contenedor sin revelar su valor en el archivo YAML?**
   a) `environment: - SECRETO=****`
   b) `environment: - SECRETO` *(Correcta: Passthrough)*
   c) `environment: - ${SECRETO}`
   d) `variable: SECRETO`

## Preguntas de Desarrollo (30 pts)

4. **Explica la diferencia técnica entre usar `${VAR}` en el `docker-compose.yml` y definir `VAR` en la sección `environment`.**
   *Rúbrica*: 10 pts por explicar que `${VAR}` es una **interpolación** que ocurre en el host (Compose reemplaza el texto antes de enviar la config a Docker), mientras que `environment` inyecta la variable dentro del **contenedor** en tiempo de ejecución.

5. **Describe el flujo de trabajo seguro para compartir un proyecto que requiere claves de API sin exponerlas en el repositorio git.**
   *Rúbrica*: 10 pts por: 1) Agregar `.env` al `.gitignore`. 2) Crear un `.env.example` con las claves vacías. 3) Subir el example. 4) Instruir al desarrollador para que copie example a `.env` y llene sus datos.

6. **¿Cómo escaparías un signo de dólar literal (`$`) en un valor de variable dentro de un archivo docker-compose.yml para evitar que Compose intente interpretarlo?**
   *Rúbrica*: 10 pts por indicar el uso del doble signo de dólar: `$$`.
