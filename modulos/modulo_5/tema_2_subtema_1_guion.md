# Guión de Audio – Límites de CPU y Memoria

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Controlador de tráfico aéreo
- **Audiencia**: Sysadmins que han visto servidores colgarse a las 3 AM

## INTRO (30 s)
Imagina que invitas a cinco amigos a comer pizza. Si no pones reglas, uno solo podría comerse las ocho porciones y dejar a los demás con hambre. En Docker pasa lo mismo: un solo contenedor malicioso o con un bug puede devorar toda la RAM de tu servidor y tumbar a todos los vecinos. Hoy aprenderemos a poner límites.

## DESARROLLO (2 min)

### 1️⃣ Memoria: El recurso crítico
- La RAM no es elástica. Si se acaba, el sistema operativo entra en pánico.
- Docker nos permite poner un **Hard Limit**.
- Ejemplo: "Tú, contenedor de base de datos, tienes 1GB. Ni un byte más".
- Si intenta cruzar esa línea, aparece el **OOM Killer** (Out of Memory Killer) y asesina el proceso. Es drástico, pero salva al resto del servidor.

### 2️⃣ CPU: El recurso elástico
- La CPU es diferente. Si se acaba, todo va más lento, pero no suele explotar.
- Con `--cpus="0.5"`, le dices a Docker: "Este contenedor solo merece la mitad de la potencia de un núcleo".
- Es ideal para procesos en segundo plano (workers) que no quieres que ralenticen tu API principal.

### 3️⃣ Monitorización
- No pongas límites a ciegas.
- Usa `docker stats` para ver cuánto consumen tus aplicaciones hoy.
- Si tu app consume 200MB, ponle un límite de 300MB o 400MB. Dale espacio para respirar, pero ponle un techo para evitar desastres.

## CIERRE (30 s)
La regla de oro en producción es: **Ningún contenedor se despliega sin límites**. Protege tu infraestructura, garantiza la calidad de servicio y duerme tranquilo sabiendo que el OOM Killer es tu guardaespaldas.

## NOTAS DE PRODUCCIÓN
- Usar un tono de "autoridad tranquila".
- Enfatizar "Ningún contenedor se despliega sin límites".
