# Evaluación – Multi-stage Builds

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es el propósito principal de un Multi-stage Build?**
   a) Compilar varios lenguajes a la vez.
   b) Crear imágenes finales más pequeñas y seguras separando la fase de construcción de la de ejecución. *(Correcta)*
   c) Acelerar la descarga de imágenes base.
   d) Permitir tener múltiples CMDs en un contenedor.

2. **¿Qué instrucción permite copiar un archivo generado en una etapa anterior?**
   a) `COPY --previous ...`
   b) `COPY --from=etapa_anterior ...` *(Correcta)*
   c) `MOVE --source=etapa_anterior ...`
   d) `IMPORT ...`

3. **¿Qué sucede con los archivos de la primera etapa (builder) que NO se copian a la segunda etapa?**
   a) Se guardan en una carpeta oculta en la imagen final.
   b) Se eliminan y no forman parte de la imagen final. *(Correcta)*
   c) Se envían al Docker Hub como caché.
   d) Provocan un error de compilación.

## Preguntas de Desarrollo (30 pts)

4. **Explica con tus palabras la analogía de la "cocina y el plato" para describir Multi-stage Builds.**
   *Rúbrica*: 10 pts por explicar que en la primera etapa (cocina) tienes todas las herramientas y "suciedad" necesaria para preparar el producto, pero al cliente (imagen final/plato) solo le entregas el resultado limpio, sin los utensilios.

5. **Menciona dos ventajas de seguridad al usar imágenes *runtime* mínimas (como Alpine o Distroless) en la etapa final.**
   *Rúbrica*: 10 pts por mencionar: 1) Menor superficie de ataque (menos paquetes vulnerables). 2) Ausencia de herramientas útiles para atacantes (shells, curl, compiladores) en la imagen final.

6. **Escribe la estructura esqueleto de un Dockerfile Multi-stage con dos etapas.**
   *Rúbrica*: 10 pts por la estructura:
   ```Dockerfile
   FROM ... AS builder
   # ... build commands ...
   FROM ...
   COPY --from=builder ...
   CMD ...
   ```
