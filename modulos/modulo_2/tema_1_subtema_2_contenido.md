# Contenido del Subtema 2 – Contexto de Build

## Objetivo

Al finalizar este subtema, serás capaz de:

1.  Entender qué es "enviar el contexto" al Daemon y por qué a veces tarda tanto.
2.  Usar **`.dockerignore`** para filtrar basura y secretos.
3.  Acelerar tus builds drásticamente ignorando carpetas pesadas como `node_modules` o `.git`.

## Contenido Teórico

### El Problema de la "Mudanza"

Cuando escribes:
`docker build .`

Docker **NO** empieza a leer tu Dockerfile inmediatamente. Lo primero que hace es una "mudanza":

1.  Toma **TODO** lo que hay en la carpeta actual (`.`).
2.  Lo empaqueta en un archivo `.tar` gigante.
3.  Se lo envía al Docker Daemon (que podría estar en otra máquina).
4.  El Daemon lo recibe, lo desempaqueta y **recién entonces** empieza a leer el Dockerfile.

**¿El problema?**
Si tienes una carpeta `node_modules` (o `vendor`) que pesa 500MB, o una carpeta `.git` gigante, Docker va a transferir esos 500MB al Daemon *cada vez* que hagas un build. Es lento y desperdicia recursos.

---

### La Solución: El archivo `.dockerignore`

Es un archivo de texto simple (muy parecido a `.gitignore`) que le dice al cliente de Docker: "Oye, antes de enviar el paquete de la mudanza, **ignora** estos archivos".

#### ¿Qué deberías ignorar SIEMPRE?

1.  **Dependencias Locales** (`node_modules`, `vendor`, `target`):
    *   *Por qué*: Queremos instalar las dependencias limpias DENTRO del contenedor (`RUN npm install`), no copiar las de tu máquina (que pueden ser incompatibles, ej. Windows vs Linux).
2.  **Sistema de Versiones** (`.git`):
    *   *Por qué*: Pesa mucho y no sirve para correr la app.
3.  **Secretos** (`.env`, claves SSH):
    *   *Por qué*: ¡Seguridad! Si copias tu `.env` a la imagen, cualquiera que tenga la imagen tendrá tus contraseñas.
4.  **Archivos Temporales** (`.DS_Store`, `npm-debug.log`).

### Ejemplo de un `.dockerignore` perfecto

```text
# Dependencias (Las instalaremos dentro, no las copiamos)
node_modules
dist
build

# Control de versiones
.git
.gitignore

# Secretos (¡Nunca los incluyas!)
.env
docker-compose.yml

# Archivos del sistema
.DS_Store
Thumbs.db
Dockerfile
README.md
```

## Paso a Paso práctico

Vamos a simular un proyecto "pesado".

1.  **Crear basura**: En tu terminal, crea un archivo "pesado" ficticio de 100MB.
    *   Linux/Mac: `mkfile 100m basura.dat` o `dd if=/dev/zero of=basura.dat bs=1M count=100`.
    *   Windows (PowerShell): `fsutil file createnew basura.dat 104857600`.

2.  **Build Lento**: Crea un Dockerfile mínimo (`FROM alpine`) y haz build:
    `docker build -t prueba-lenta .`
    *   *Observa*: El mensaje "Sending build context to Docker daemon" tardará unos segundos y mostrará un tamaño grande (approx 100MB).

3.  **Arreglarlo**: Crea un archivo `.dockerignore` y escribe dentro:
    ```
    basura.dat
    ```

4.  **Build Rápido**: Repite el build.
    `docker build -t prueba-rapida .`
    *   *Observa*: ¡Instantáneo! El contexto enviado será de unos pocos bytes.

## Resumen

*   Antes de cocinar, Docker "hace la compra" de todos los archivos de tu carpeta.
*   Si la compra es enorme (archivos basura), la cocina tarda en empezar.
*   Usa **`.dockerignore`** para dejar fuera lo que no sirve (y lo que es peligroso).
*   **Regla de oro**: Si está en `.gitignore`, probablemente debería estar en `.dockerignore`.
