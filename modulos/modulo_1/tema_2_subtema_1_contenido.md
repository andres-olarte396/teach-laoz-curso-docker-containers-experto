# Contenido del Subtema 1 – Instalación y Hola Mundo

## Objetivo

Al finalizar este subtema, serás capaz de:

1.  Instalar Docker en tu sistema operativo (Windows WSL2, macOS o Linux).
2.  Ejecutar tu primer contenedor (`docker run hello-world`).
3.  Entender qué significa "Permission Denied" y cómo solucionarlo.

## Contenido Teórico

### 1️⃣ Instalación: Elige tu camino

La instalación varía según tu sistema, pero el resultado es el mismo: tendrás el comando `docker` disponible.

#### Opción A: Windows y Mac (Docker Desktop)
La forma más fácil. Es una aplicación gráfica que instala todo por ti (Cliente, Daemon, Linux virtual).
*   **Descarga**: Ve a [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop).
*   **Requisito Windows**: Te pedirá usar **WSL2** (Windows Subsystem for Linux). Acepta todo. Es la tecnología que permite correr Linux dentro de Windows de forma nativa.

#### Opción B: Linux (Servidores o Desktop)
Aquí instalamos el motor nativo directamente sobre el sistema.

**Método Rápido (Recomendado para estudiantes)**:
Usa el script oficial de instalación automática:
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

**Método Manual (Producción)**:
Implica configurar repositorios GPG y apt, como viste en versiones anteriores. Se recomienda solo para entornos controlados de producción.

---

### 2️⃣ El problema del "Acceso Denegado" (Linux)

Si después de instalar, escribes `docker version` y ves este error:
`Got permission denied while trying to connect to the Docker daemon socket`

**¿Qué pasó?**
El **Daemon** (el Chef) es un proceso muy poderoso que corre como **root** (Administrador Supremo). Tú, como usuario mortal, no tienes permiso para hablarle.

**Solución**:
Únete al grupo VIP llamado `docker`.
```bash
sudo usermod -aG docker $USER
```
*Importante*: Debes cerrar sesión y volver a entrar (o reiniciar) para que el carnet del club VIP se active.

---

### 3️⃣ Tu primer contenedor: `hello-world`

El rito de iniciación. Ejecuta:
```bash
docker run hello-world
```

**Si todo sale bien, verás esto (y te explicamos qué significa):**

1.  `Unable to find image 'hello-world:latest' locally`
    *   *Traducción*: "Busqué en mi cocina y no encontré la receta de Hello World".
2.  `Pulling from library/hello-world`
    *   *Traducción*: "Yendo al supermercado (Docker Hub) a descargarla".
3.  `Hello from Docker!`
    *   *Traducción*: ¡Éxito! El contenedor se creó, ejecutó su mensaje y se apagó.

## Resumen

*   En **Windows/Mac** usas Docker Desktop. En **Linux** usas el Engine nativo.
*   En Linux, recuerda agregar tu usuario al grupo `docker` para no usar `sudo` todo el tiempo.
*   `docker run` hace todo el trabajo: descargar, crear y ejecutar.
