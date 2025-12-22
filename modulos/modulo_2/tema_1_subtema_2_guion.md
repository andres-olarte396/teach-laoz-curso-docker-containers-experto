# Guión de Audio – Contexto de Build

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Práctico y preventivo
- **Audiencia**: Desarrolladores que buscan optimizar sus tiempos de build

## INTRO (30 s)
¿Alguna vez has visto el mensaje "Sending build context to Docker daemon" quedarse pegado por segundos... o minutos? Hoy vamos a solucionar eso. Hablaremos del **Contexto de Build** y su mejor amigo: el archivo **.dockerignore**.

## DESARROLLO (2 min)

### 1️⃣ ¿Qué es el Contexto?
- Cuando ejecutas `docker build .`, ese puntito final no es adorno. Le dice a Docker: "Empaqueta TODO lo que hay en esta carpeta y envíaselo al motor".
- Si tienes carpetas como `node_modules`, `.git` o archivos temporales pesados, Docker los copia **antes** de leer siquiera la primera línea de tu Dockerfile.
- Resultado: Builds lentos y desperdicio de red/disco.

### 2️⃣ La Solución: .dockerignore
- Este archivo es idéntico al `.gitignore` pero para Docker.
- Todo lo que listes aquí, Docker lo ignorará por completo al crear el contexto.
- **Regla de oro**: Siempre ignora `.git`, archivos de dependencias locales (`node_modules`, `vendor`), archivos de entorno (`.env`) y logs.

### 3️⃣ Seguridad y Caché
- Además de velocidad, ganas seguridad. Si ignoras `.env`, es imposible que tus claves secretas terminen copiadas por error en la imagen final.
- También mejora la caché: si cambias un archivo ignorado (como el README), Docker no invalidará las capas de tu imagen.

## CIERRE (30 s)
Un `.dockerignore` bien configurado es la diferencia entre un build instantáneo y uno que te da tiempo de ir por café. ¡Configúralo en cada proyecto! Ahora, a practicar con los ejercicios.

## NOTAS DE PRODUCCIÓN
- Insertar pausa de 1s entre secciones.
- Enfatizar que el contexto se envía *antes* del build.
