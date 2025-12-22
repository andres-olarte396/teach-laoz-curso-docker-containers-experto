# Guión de Audio – Instrucciones Clave de Dockerfile

## Metadata
- **Duración estimada**: 4 minutos
- **Tono**: Técnico pero accesible
- **Audiencia**: Desarrolladores que inician en la creación de imágenes

## INTRO (30 s)
¡Bienvenido al Módulo 2! Aquí es donde la magia ocurre. Vamos a aprender a escribir **Dockerfiles**, las recetas que Docker usa para cocinar tus imágenes.

## DESARROLLO (2 min)

### 1️⃣ La Base: FROM y WORKDIR
- Todo empieza con **`FROM`**. Define de qué imagen partes (por ejemplo, `ubuntu` o `node`). Es el cimiento de tu casa.
- Luego, **`WORKDIR`**. Es como hacer `cd` en la terminal. Define dónde pondrás tus archivos. ¡Úsalo siempre para mantener el orden!

### 2️⃣ Moviendo archivos: COPY vs ADD
- Para meter tu código al contenedor, usa **`COPY`**. Es simple y directo.
- Existe **`ADD`**, que tiene superpoderes como descomprimir archivos, pero úsalo con cuidado. Para el 99% de los casos, `COPY` es lo que buscas.

### 3️⃣ Ejecutando acciones: RUN
- **`RUN`** ejecuta comandos *durante la construcción*. Instalar librerías, compilar código… todo eso va con `RUN`. Recuerda: cada `RUN` crea una capa nueva, así que intenta agruparlos.

### 4️⃣ El Arranque: CMD vs ENTRYPOINT
- ¿Qué hace el contenedor al iniciarse?
- **`CMD`** es el comando por defecto. Si el usuario escribe otro comando al correr `docker run`, el `CMD` se ignora.
- **`ENTRYPOINT`** es más estricto. Define el ejecutable principal y lo que el usuario escriba se añade como argumentos.
- Truco pro: Usa `ENTRYPOINT` para tu binario y `CMD` para los parámetros por defecto.

## CIERRE (30 s)
Dominar estas instrucciones es la clave para crear imágenes robustas. Un buen Dockerfile es legible y eficiente. ¡Vamos a escribir el tuyo en los ejercicios!

## NOTAS DE PRODUCCIÓN
- Insertar pausa de 1.5s entre las explicaciones de las instrucciones.
- Enfatizar la distinción entre *tiempo de construcción* (RUN) y *tiempo de ejecución* (CMD).
