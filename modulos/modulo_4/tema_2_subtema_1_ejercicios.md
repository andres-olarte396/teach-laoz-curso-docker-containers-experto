# Ejercicios – Development vs Production

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Visualizando el Merge**
1. Crea `docker-compose.yml`:
   ```yaml
   services:
     app:
       image: alpine
       command: echo "Base"
   ```
2. Crea `docker-compose.override.yml`:
   ```yaml
   services:
     app:
       command: echo "Override"
   ```
3. Ejecuta `docker compose config`. ¿Qué comando final muestra?
4. Ejecuta `docker compose up`. ¿Qué imprime?

**Ejercicio 2 – Entorno de Producción**
1. Crea `prod.yml`:
   ```yaml
   services:
     app:
       restart: always
   ```
2. Ejecuta `docker compose -f docker-compose.yml -f prod.yml config`.
3. Verifica que `restart: always` aparece en la configuración final combinada.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Simulando un flujo real**
1. Tienes una app Node/Python.
2. En el archivo base, define la imagen `base` y la red.
3. En el override (dev), define un volumen `./:/app` y el comando de inicio en modo "watch" (ej. `nodemon` o `flask run --reload`).
4. En el archivo prod, define `restart: always` y elimina el volumen (para usar el código copiado dentro de la imagen).
5. Levanta ambos entornos y compara: en Dev, si cambias un archivo local, la app se reinicia. En Prod, no.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 4 – Puertos diferentes**
1. Configura tu app para que en Desarrollo escuche en el puerto `8080:80` (para no chocar con otros servicios).
2. Configura Producción para que escuche en `80:80`.
3. Levanta Dev y prueba `localhost:8080`.
4. Levanta Prod y prueba `localhost:80`.

**Ejercicio 5 – Perfiles (Profiles)**
1. Investiga el feature `profiles` de Docker Compose.
2. Agrega un servicio `phpmyadmin` o `pgadmin` al archivo compose pero asígnale `profiles: ["debug"]`.
3. Ejecuta `docker compose up` normal. ¿Arranca adminer?
4. Ejecuta `docker compose --profile debug up`. ¿Arranca ahora?
   *Esto es utilísimo para herramientas que solo necesitas a veces.*
