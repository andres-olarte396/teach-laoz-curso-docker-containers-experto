# Guión de Audio – Multi-stage Builds

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Profesional y revelador
- **Audiencia**: Desarrolladores cansados de imágenes pesadas

## INTRO (30 s)
¿Tus imágenes Docker pesan cientos de megas solo para correr un "Hola Mundo"? Es hora de poner tus Dockerfiles a dieta. Hoy aprenderemos el patrón más importante para producción: **Multi-stage Builds**.

## DESARROLLO (2 min)

### 1️⃣ El Problema de la Obesidad Digital
- Imagina que para servir una taza de café, tuvieras que llevar la cafetera, el molino y el saco de granos a la mesa. Eso hacemos cuando incluimos el compilador (como GCC o Go) en la imagen final.
- Resultado: Imágenes lentas de subir, caras de almacenar y llenas de vulnerabilidades potenciales.

### 2️⃣ La Magia de Multi-stage
- Con Multi-stage, usamos un solo Dockerfile pero con varias instrucciones `FROM`.
- La primera etapa es la **cocina**: tiene todas las herramientas, compila el código y genera el binario.
- La segunda etapa es el **plato**: es una imagen vacía o mínima (como Alpine) donde solo copiamos el binario final desde la cocina.
- Todo lo demás (compiladores, código fuente) se descarta.

### 3️⃣ Distroless: El siguiente nivel
- Puedes llevar esto al extremo usando imágenes "Distroless". No tienen ni siquiera sistema operativo ni shell. Solo tu aplicación.
- Son ultra ligeras y muy seguras, porque un atacante no tiene herramientas para moverse si logra entrar.

## CIERRE (30 s)
Multi-stage build no es opcional si vas a producción. Es la diferencia entre un despliegue profesional y uno amateur. Reduce costos, tiempos y riesgos. ¡Pruébalo ahora en los ejercicios y sorpréndete con la diferencia de tamaño!

## NOTAS DE PRODUCCIÓN
- Insertar pausa tras la analogía del café.
- Enfatizar "se descarta" para reforzar la idea de limpieza.
