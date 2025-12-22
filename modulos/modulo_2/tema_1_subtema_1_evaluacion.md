# Evaluación – Instrucciones Clave

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué instrucción se utiliza para definir el directorio de trabajo dentro de la imagen?**
   a) `CD`
   b) `DIR`
   c) `WORKDIR` *(Correcta)*
   d) `PLACE`

2. **¿Cuál es la diferencia principal entre `RUN` y `CMD`?**
   a) `RUN` se ejecuta al iniciar el contenedor, `CMD` al construir la imagen.
   b) `RUN` se ejecuta durante la construcción (build), `CMD` define el comando de inicio del contenedor. *(Correcta)*
   c) No hay diferencia, son alias.
   d) `RUN` es para Linux, `CMD` para Windows.

3. **Si tienes un Dockerfile con `COPY . .`, ¿qué hace esta instrucción?**
   a) Copia todo internet al contenedor.
   b) Copia los archivos del directorio actual del host al directorio de trabajo de la imagen. *(Correcta)*
   c) Duplica la imagen base.
   d) Copia los archivos del contenedor al host.

## Preguntas de Desarrollo (30 pts)

4. **Explica cuándo deberías usar `COPY` y cuándo `ADD`. ¿Por qué se prefiere `COPY`?**
   *Rúbrica*: 10 pts por indicar que `COPY` es solo para archivos locales y es más transparente. `ADD` tiene funciones "mágicas" (tar, url remote) que pueden ser inseguras o confusas si no se necesitan.

5. **Describe el patrón de uso combinado de `ENTRYPOINT` y `CMD`.**
   *Rúbrica*: 10 pts por explicar que `ENTRYPOINT` fija el ejecutable (inmutable) y `CMD` provee los argumentos por defecto (sobre-escribibles por el usuario).

6. **Escribe un Dockerfile mínimo para una aplicación Node.js que vive en `/app`, copia `package.json`, instala dependencias y arranca con `node server.js`.**
   *Rúbrica*: 10 pts por la estructura correcta: `FROM`, `WORKDIR`, `COPY`, `RUN`, `CMD`.
