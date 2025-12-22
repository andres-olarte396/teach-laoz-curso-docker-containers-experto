# Ejercicios – Multi-stage Builds

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Comparación de tamaños**
1. Crea un archivo `main.go`:
   ```go
   package main
   import "fmt"
   func main() { fmt.Println("Hola Multi-stage") }
   ```
2. Crea un `Dockerfile.single` usando solo `FROM golang:1.21` y compilando dentro.
3. Construye la imagen: `docker build -f Dockerfile.single -t monolitico .`.
4. Revisa el tamaño con `docker images monolitico`.
5. Anota el tamaño (debería ser cientos de MB).

## Nivel Intermedio (≈ 10 min)

**Ejercicio 2 – Implementando Multi-stage**
1. Crea un `Dockerfile.multi` basado en el ejemplo del contenido teórico:
   - Stage 1: `golang:1.21` (alias `builder`) → compila `main.go`.
   - Stage 2: `alpine` → copia el binario.
2. Construye: `docker build -f Dockerfile.multi -t optimizado .`.
3. Compara el tamaño con la imagen `monolitico`.
4. Ejecuta `docker run optimizado` para verificar que funciona.

**Ejercicio 3 – Node.js y Multi-stage**
A veces no es un binario, sino dependencias de producción vs desarrollo.
1. Crea un `package.json`.
2. Escribe un Dockerfile con dos etapas:
   - **build**: `RUN npm install` (instala todo).
   - **production**: Copia `node_modules` desde build, o ejecuta `npm install --only=production`.
   *(Nota: En Node es más común copiar el build output si usas TypeScript/Webpack)*.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 4 – Distroless**
1. Modifica el Dockerfile del Ejercicio 2.
2. En lugar de `FROM alpine`, usa `FROM gcr.io/distroless/static-debian11`.
3. Construye y verifica el tamaño y funcionamiento.
4. Intenta entrar con `docker exec -it ... sh`. ¿Puedes? (Spoiler: No, no hay shell).
5. Explica por qué esto es bueno para la seguridad.

**Ejercicio 5 – Multi-target**
1. Investiga cómo usar `--target` al hacer build.
2. Modifica tu Dockerfile para tener una etapa intermedia `test` que corra pruebas unitarias.
3. Ejecuta el build apuntando solo al target de prueba: `docker build --target test .`.
