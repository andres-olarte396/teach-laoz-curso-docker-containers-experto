# Guión de Audio – Instalación y Hola Mundo

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Entusiasta y Práctico
- **Audiencia**: Principiantes absolutos

## INTRO (30 s)
¡Bienvenido a la práctica! Ya conoces la teoría, ahora vamos a ensuciarnos las manos. En esta lección instalaremos Docker y ejecutaremos tu primer contenedor. Es el momento "Hola Mundo" que todo ingeniero recuerda.

## DESARROLLO (2 min)

### 1️⃣ La Instalación
- Si estás en Windows o Mac, usarás **Docker Desktop**. Es una aplicación todo-en-uno que incluye el Engine, el Cliente y una interfaz gráfica.
- Si estás en Linux, instalaremos el **Docker Engine** nativo. Es más ligero y es lo que usarás en servidores de producción.
- Una vez instalado, la prueba de fuego es abrir tu terminal y escribir: `docker version`. Si ves la versión del Cliente y del Servidor, ¡estás dentro!

### 2️⃣ Hola Mundo
- Vamos a correr el comando sagrado: `docker run hello-world`.
- ¿Qué acaba de pasar?
- Docker no encontró la imagen en tu disco.
- Fue a internet (Docker Hub).
- La descargó.
- Creó un contenedor.
- El contenedor ejecutó un script que imprimió el mensaje de bienvenida.
- Y finalmente, el contenedor se apagó. Todo eso en segundos.

### 3️⃣ Docker Hub
- ¿De dónde salió esa imagen? De Docker Hub, la "App Store" de los contenedores.
- Allí encontrarás imágenes oficiales para todo: Python, Node.js, MySQL, lo que necesites.

## CIERRE (30 s)
Felicidades, ya no hay vuelta atrás. Tienes el poder de la containerización en tu máquina. En las próximas lecciones, dejaremos de correr ejemplos simples y empezaremos a trabajar con aplicaciones reales. ¡A seguir!

## NOTAS DE PRODUCCIÓN
- Transmitir emoción al describir el proceso de `docker run hello-world`.
