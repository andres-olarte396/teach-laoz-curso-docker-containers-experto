# Guión de Audio – Ciclo de vida básico

## Metadata
- **Duración estimada**: 4 minutos
- **Tono**: Práctico, directo, profesional
- **Audiencia**: Desarrolladores aprendiendo Docker

## INTRO (30 s)
¡Bienvenido! Ahora que ya tienes Docker instalado, vamos a dominar el ciclo de vida de los contenedores. Aprenderás a crearlos, detenerlos, inspeccionarlos y eliminarlos con total confianza.

## DESARROLLO (2 min)

### 1️⃣ Crear e Iniciar (`run` vs `start`)
- **`docker run`** es el comando estrella. Crea el contenedor y lo inicia.
- Usa el flag `-d` para liberarte de la terminal y correrlo en segundo plano.
- Asigna siempre un nombre con `--name` para no tener que lidiar con IDs aleatorios.

### 2️⃣ Detener y Reiniciar
- Cuando termines, usa **`docker stop`**. Envía una señal amable para cerrar procesos.
- Si algo falla o cambias configuración, **`docker restart`** es tu amigo.

### 3️⃣ Inspección (`ps`, `logs`, `exec`)
- ¿Qué está pasando? **`docker ps`** te muestra los activos. Agrega `-a` para ver los detenidos.
- ¿Errores? **`docker logs`** te muestra la salida estándar.
- ¿Necesitas entrar? **`docker exec -it <nombre> bash`** te da una terminal dentro del contenedor. ¡Es como SSH pero mejor!

### 4️⃣ Limpieza (`rm`)
- Los contenedores detenidos ocupan espacio.
- Usa **`docker rm`** para borrarlos.
- Ojo con `--rm` en `docker run`: elimina el contenedor automáticamente al salir, ideal para pruebas rápidas.

## CIERRE (30 s)
Gestionar el ciclo de vida es la habilidad que usarás todos los días. Acostúmbrate a nombrar tus contenedores y a mantener tu entorno limpio. ¡A practicar con los ejercicios!

## NOTAS DE PRODUCCIÓN
- Insertar pausa de 1 s entre comandos explicados.
- Enfatizar la diferencia entre *run* (nuevo) y *start* (existente).
```
