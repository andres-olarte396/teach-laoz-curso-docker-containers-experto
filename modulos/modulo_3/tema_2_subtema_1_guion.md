# Guión de Audio – Tipos de Monturas

## Metadata
- **Duración estimada**: 4 minutos
- **Tono**: Explicativo y comparativo
- **Audiencia**: Devs que no quieren perder sus datos

## INTRO (30 s)
Los contenedores son efímeros. Si borras un contenedor, sus datos desaparecen para siempre... a menos que uses **Monturas**. Hoy aprenderemos a guardar lo que importa.

## DESARROLLO (2 min 30 s)

### 1️⃣ El Menú de Opciones
Docker nos da tres herramientas. Elegir la correcta es vital.
- **Volúmenes (Volumes)**: Son la opción nativa de Docker. Viven en una "caja fuerte" dentro de Docker. Son perfectos para bases de datos.
- **Bind Mounts**: Son un puente directo a tus carpetas personales. Lo que cambias en tu escritorio, cambia en el contenedor. Son ideales para desarrollar y ver cambios en tiempo real.
- **tmpfs**: Son discos en memoria RAM. Rápidos como el rayo, pero volátiles. Úsalos para cosas que no quieres guardar, como secretos descifrados.

### 2️⃣ La Sintaxis: `-v` vs `--mount`
- Verás muchos tutoriales viejos usando `-v` (menos uve). Funciona, pero es confuso.
- Te recomiendo usar **`--mount`**.
- ¿Por qué? Porque es explícito. Dices claramente `type=volume` o `type=bind`. Además, si te equivocas de ruta en un bind mount, `-v` crea una carpeta vacía y te confunde, mientras que `--mount` te avisa del error.

### 3️⃣ Caso de Uso Real
- Imagina que programas una web. Usas un **Bind Mount** para el código fuente, así editas y ves los cambios.
- Pero tu base de datos usa un **Volumen**, para que los datos sobrevivan aunque destruyas el contenedor de la DB.
- Y las claves de sesión temporales, van a **tmpfs**.

## CIERRE (30 s)
Recuerda: Contenedor borrado = datos perdidos, SALVO que uses monturas. Practica creando un volumen y un bind mount en los ejercicios. ¡Verás que la persistencia te da paz mental!

## NOTAS DE PRODUCCIÓN
- Insertar pausa clara entre los tres tipos de monturas.
- Enfatizar "Volúmenes para Producción" y "Bind Mounts para Desarrollo".
