# Guión de Audio – Gestión de Caché

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Estratégico y eficiente
- **Audiencia**: Desarrolladores que odian esperar a que termine el build

## INTRO (30 s)
El tiempo es oro. Si tu build tarda 10 minutos cada vez que cambias una línea de código, estás perdiendo horas a la semana. El secreto para builds instantáneos es entender la **Caché de Docker**.

## DESARROLLO (2 min)

### 1️⃣ El Efecto Dominó
- Docker construye por capas. Si una capa no cambia, Docker usa la versión cacheada. ¡Genial!
- Pero aquí está el truco: Si una capa cambia, **todas las capas que siguen se invalidan**.
- Es como construir una torre de bloques. Si cambias el bloque de abajo, tienes que reconstruir todo lo que está encima.

### 2️⃣ Patrones de Oro
- Lo que cambia menos a menudo debe ir arriba.
- Lo que cambia frecuentemente (tu código fuente) debe ir abajo.
- Por eso, **siempre** copia tus archivos de dependencias (`package.json`, `requirements.txt`) e instálalos **antes** de copiar el resto del código (`COPY . .`).

### 3️⃣ Trucos Pro: Cache Mounts
- A veces, incluso con buen orden, invalidas la caché y tienes que bajar todo de nuevo.
- Con **BuildKit** y `Cache Mounts`, puedes decirle a Docker: "Guarda esta carpeta de descargas (`.npm`, `.pip`) en un lugar seguro".
- Así, aunque reconstruyas la capa, no tienes que volver a descargar internet entero.

## CIERRE (30 s)
Un Dockerfile bien ordenado es una obra de ingeniería. Ahorra tiempo, ancho de banda y paciencia. Revisa tus proyectos hoy mismo y reorganiza esas instrucciones. ¡Verás la diferencia al instante!

## NOTAS DE PRODUCCIÓN
- Insertar pausa de 1s entre puntos.
- Usar tono de advertencia en "todas las capas que siguen se invalidan".
