# Evaluación – Gestión de Caché

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **Si modificas un archivo copiado en la línea 3 de tu Dockerfile, ¿qué sucede con las instrucciones de la línea 4 en adelante?**
   a) Se reutilizan de la caché.
   b) Se invalidan y se ejecutan de nuevo. *(Correcta)*
   c) Docker pregunta si quieres reconstruirlas.
   d) Solo se ejecuta la línea 4, las demás se saltan.

2. **¿Cuál es el orden ideal para estas instrucciones en una app Node.js?**
   a) `COPY . .` → `RUN npm install`
   b) `RUN npm install` → `COPY . .`
   c) `COPY package.json .` → `RUN npm install` → `COPY . .` *(Correcta)*
   d) `WORKDIR /app` → `CMD node app.js`

3. **¿Qué problema resuelve agrupar `apt-get update && apt-get install` en una sola línea `RUN`?**
   a) Ahorra espacio en disco.
   b) Evita que Docker use una caché obsoleta de `apt-get update` al instalar nuevos paquetes. *(Correcta)*
   c) Hace que el build sea más rápido.
   d) Permite instalar paquetes de Windows en Linux.

## Preguntas de Desarrollo (30 pts)

4. **Explica por qué el comando `COPY . .` debería estar cerca del final del Dockerfile.**
   *Rúbrica*: 10 pts por razonar que el código fuente cambia con mucha frecuencia (en cada commit), y si se pone al principio, invalidará la caché de todas las instrucciones subsiguientes (como la instalación de dependencias), ralentizando el build.

5. **Describe qué es un "Cache Mount" (--mount=type=cache) y un caso de uso.**
   *Rúbrica*: 10 pts por explicar que permite persistir un directorio (como `/root/.npm` o `/var/cache/apt`) entre compilaciones, incluso si la capa Docker se invalida, evitando descargas repetitivas.

6. **¿Cómo puedes forzar la invalidación de caché para una instrucción específica (ej. un `git clone`) sin cambiar el Dockerfile?**
   *Rúbrica*: 10 pts por mencionar el uso de Argumentos de Build (`ARG`) que se pasan al construir con un valor dinámico (ej. fecha/hora), cambiando el entorno de esa instrucción y forzando su ejecución.
