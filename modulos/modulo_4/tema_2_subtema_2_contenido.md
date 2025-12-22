# Contenido del Subtema 2 – Variables de Entorno

## Objetivo

Al finalizar este subtema, serás capaz de:

1.  Hacer que tu proyecto sea flexible y configurable sin tocar el código.
2.  Proteger tus secretos (contraseñas) para que no terminen en GitHub.
3.  Entender la diferencia entre "Configurar Docker" y "Configurar tu App".

## Contenido Teórico

### El Problema del Hard-Coding

Imagina que pones tu contraseña de base de datos directa en el archivo `docker-compose.yml`.
Resulta que subes ese archivo a GitHub público.
**Felicidades, te han hackeado.**

Para evitar esto, usamos **Variables de Entorno**. Son valores que viven *fuera* del código.

---

### Los Dos Momentos de las Variables

Esto confunde a todos. Hay dos lugares donde puedes usar variables:

#### Momento 1: Configurando a Docker (Interpolación)
Esto sucede **ANTES** de que Docker arranque nada. Docker lee tu archivo YAML y rellena los huecos `${...}` con lo que encuentre en el archivo `.env`.

*   **Archivo `.env`**:
    ```bash
    VERSION_IMAGEN=v2.0
    PUERTO_PC=8080
    ```

*   **Archivo `docker-compose.yml`**:
    ```yaml
    services:
      web:
        image: mi-app:${VERSION_IMAGEN}  # Docker lee: mi-app:v2.0
        ports:
          - "${PUERTO_PC}:80"            # Docker lee: "8080:80"
    ```

#### Momento 2: Configurando tu App (Runtime)
Esto es para pasarle datos a tu código (Node.js, Python, PHP) para que los lea con `process.env.ALGO`.

*   **Opción A: Inyección Directa (`environment`)**:
    ```yaml
    services:
      web:
        environment:
          - DB_PASSWORD=secreto_nuclear
    ```
    *Desventaja*: Sigues escribiendo el secreto en el YAML.

*   **Opción B: Passthrough (La mejor)**:
    ```yaml
    services:
      web:
        environment:
          - DB_PASSWORD  # ¡Sin valor!
    ```
    Docker buscará `DB_PASSWORD` en tu máquina (o en el archivo `.env`) y se la pasará al contenedor.

*   **Opción C: Archivo Completo (`env_file`)**:
    "Toma este archivo lleno de secretos y dáselo al contenedor".
    ```yaml
    services:
      web:
        env_file:
          - .env.production
    ```

---

### Seguridad: El `.gitignore`

Si usas un archivo `.env` con secretos reales, **TIENES QUE IGNORARLO EN GIT**.

1.  Crea un archivo `.env` con tus claves reales. (Ponlo en `.gitignore`).
2.  Crea un archivo `.env.example` con claves falsas (`PASSWORD=cambiame`). (Súbelo a Git).
3.  Tus compañeros bajarán el proyecto, copiarán el example y pondrán sus propias claves.

## Paso a Paso práctico

1.  Crea una carpeta.
2.  Crea un archivo `.env` que diga: `SALUDO=Hola Mundo Secreto`.
3.  Crea un `docker-compose.yml`:
    ```yaml
    services:
      prueba:
        image: alpine
        command: echo "${SALUDO}"  # Interpolación
    ```
4.  Ejecuta `docker compose up`. Verás "Hola Mundo Secreto" en los logs.
5.  Ahora intenta pasarla al entorno:
    ```yaml
    services:
      prueba:
        image: alpine
        environment:
          - MENSAJE=${SALUDO}
        command: env  # Listar variables
    ```
    Verás que `MENSAJE` existe dentro del contenedor.

## Resumen

*   **`.env`**: Archivo mágico que Docker lee automáticamente para rellenar huecos en el YAML.
*   **`${VARIABLE}`**: Así se usa una variable en YAML.
*   **`.gitignore`**: El lugar donde debe vivir tu archivo `.env` real.
