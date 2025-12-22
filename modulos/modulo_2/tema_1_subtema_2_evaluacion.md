# Evaluación – Contexto de Build

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué sucede inmediatamente después de ejecutar `docker build .`?**
   a) Docker ejecuta la instrucción `FROM`.
   b) Docker descarga las imágenes base.
   c) El cliente Docker envía todo el contenido del directorio actual (contexto) al daemon. *(Correcta)*
   d) Docker busca el archivo `.dockerignore`.

2. **¿Cuál es el propósito principal del archivo `.dockerignore`?**
   a) Ignorar errores de compilación.
   b) Excluir archivos del contexto de build para mejorar velocidad y seguridad. *(Correcta)*
   c) Evitar que los contenedores se comuniquen con internet.
   d) Ignorar actualizaciones de Docker.

3. **Si tienes un archivo `.env` con contraseñas en tu carpeta de proyecto y ejecutas `COPY . .` en tu Dockerfile:**
   a) Docker lo ignora automáticamente porque es un archivo oculto.
   b) El archivo se copiará a la imagen, exponiendo tus secretos. *(Correcta)*
   c) Docker cifrará el archivo automáticamente.
   d) El build fallará por seguridad.

## Preguntas de Desarrollo (30 pts)

4. **Explica por qué tener una carpeta `.git` grande afecta el tiempo de build, incluso si no la usas dentro del Dockerfile.**
   *Rúbrica*: 10 pts por explicar que el contexto se envía completo al daemon *antes* de procesar el Dockerfile, por lo que transferir megabytes (o gigabytes) de historial git consume tiempo innecesariamente.

5. **Escribe un `.dockerignore` básico para un proyecto Node.js.**
   *Rúbrica*: 10 pts por incluir al menos: `node_modules`, `.git`, `.env`, `Dockerfile`, `npm-debug.log`.

6. **¿Cómo afecta el `.dockerignore` a la caché de capas de Docker?**
   *Rúbrica*: 10 pts por explicar que si se modifican archivos que están ignorados, Docker no invalida la caché de la instrucción `COPY`, lo que acelera recompilaciones innecesarias.
