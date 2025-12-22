# Ejercicios – Instalación y Hola Mundo

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Instalación en Windows**
1. Descarga Docker Desktop desde la página oficial.
2. Instala Docker Desktop asegurándote de habilitar la integración con **WSL 2**.
3. Abre una terminal PowerShell y ejecuta `docker version`.
4. Captura una captura de pantalla del resultado y verifica que aparecen tanto el **Client** como el **Server**.

**Ejercicio 2 – Instalación en macOS**
1. Descarga Docker Desktop para Mac.
2. Instálalo arrastrando el icono a la carpeta **Aplicaciones**.
3. Ejecuta `docker run hello-world` desde la Terminal.
4. Anota cualquier mensaje de error y su solución (por ejemplo, permisos de Docker Desktop).

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Instalación en Ubuntu/Debian**
```bash
sudo apt-get update
sudo apt-get install \
  ca-certificates \
  curl \
  gnupg \
  lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER
newgrp docker
```
1. Ejecuta los comandos anteriores paso a paso.
2. Verifica la instalación con `docker run hello-world`.
3. Describe en un párrafo breve qué hace cada bloque del script.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 4 – Diagnóstico de fallos comunes**
1. Simula que el daemon no está corriendo (`sudo systemctl stop docker`).
2. Intenta ejecutar `docker ps` y captura el mensaje de error.
3. Soluciona el problema reiniciando el daemon (`sudo systemctl start docker`).
4. Repite el proceso en Windows deshabilitando Docker Desktop y volviéndolo a habilitar.

**Ejercicio 5 – Configuración de WSL 2**
1. En Windows, abre PowerShell y ejecuta `wsl --set-default-version 2`.
2. Instala una distribución Linux (Ubuntu) desde la Microsoft Store.
3. Dentro de la distribución, instala Docker siguiendo los pasos de Ubuntu.
4. Ejecuta `docker run hello-world` y verifica que funciona.
5. Documenta los pasos y cualquier error encontrado.
