# Ejercicios – Contexto de Build

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Medir el impacto del contexto**
1. En una carpeta nueva, genera un archivo de 50MB:
   - Linux/Mac: `mkfile 50m dummyfile` o `dd if=/dev/zero of=dummyfile bs=1M count=50`.
   - Windows (PowerShell): `fsutil file createnew dummyfile 52428800`.
2. Crea un `Dockerfile` con `FROM alpine` y `COPY . .`.
3. Ejecuta `time docker build -t contexto-lento .` (o `Measure-Command { docker build ... }` en PS).
4. Crea un `.dockerignore` y agrega `dummyfile`.
5. Repite el build y compara el tiempo de "Sending build context".

**Ejercicio 2 – Ignorar secretos**
1. Crea un archivo `.env` con `API_KEY=supersecreto`.
2. Crea un Dockerfile que haga `COPY . .` y luego `RUN cat .env`.
3. Construye la imagen y verifica que puedes ver el secreto en el log del build.
4. Agrega `.env` al `.dockerignore`.
5. Intenta construir de nuevo. Debería fallar el `cat .env` (o no mostrar nada si el archivo no se copió), demostrando que es seguro.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Exclusiones con excepciones**
1. Crea una estructura de carpetas:
   ```
   logs/
     app.log
     error.log
     important.log
   ```
2. Configura `.dockerignore` para ignorar toda la carpeta `logs/` PERO incluir `logs/important.log` (pista: usa `!`).
3. Verifica con un build y `RUN ls -R logs` qué archivos terminaron en la imagen.

**Ejercicio 4 – Contexto remoto (Git)**
1. Intenta construir una imagen directamente desde un repositorio público de GitHub sin clonarlo:
   `docker build https://github.com/docker-library/hello-world.git`
2. Explica qué se usa como contexto en este caso.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Depurando el contexto**
A veces no estamos seguros de qué se está enviando.
1. Crea un Dockerfile de depuración:
   ```Dockerfile
   FROM alpine
   COPY . /context
   RUN du -ah /context | sort -hr | head -n 10
   ```
2. Úsalo en una carpeta de tu proyecto real (o simula una con archivos variados) para identificar qué archivos están "inflando" tu contexto innecesariamente.
