# Guión de Audio – DNS y Descubrimiento de Servicios

## Metadata
- **Duración estimada**: 4 minutos
- **Tono**: Didáctico, claro, motivador
- **Audiencia**: Desarrolladores con conocimientos básicos de Docker

## INTRO (30 s)
¡Hola! En este subtema exploraremos cómo Docker gestiona el **DNS interno** y el **service discovery**, dos pilares esenciales para que los contenedores se encuentren y se comuniquen de forma automática. Ya no necesitas memorizar IPs.

## DESARROLLO (2 min)

### 1️⃣ DNS interno de Docker
- Cada vez que creas una red de usuario (como bridge), Docker levanta un servidor DNS interno (en la IP mágica `127.0.0.11`).
- Este servidor conoce a todos los contenedores de esa red por su nombre.
- Si llamas a tu base de datos "postgres-prod", tu API solo tiene que intentar conectar a "postgres-prod". Docker hará la traducción automáticamente.
- Puedes añadir **alias** extra con `--network-alias`, útil para migraciones o nombres genéricos como "db-master".

### 2️⃣ Service Discovery en Swarm / Overlay
- Cuando das el salto a clusters con Swarm, esto se vuelve aún más potente.
- Creas un servicio con 5 réplicas llamado "web".
- Docker crea una IP Virtual (VIP) única para "web".
- Cuando alguien llama a "web", Docker recibe la petición y la balancea automáticamente entre las 5 réplicas. ¡Balanceo de carga gratis!

### 3️⃣ Buenas Prácticas
- Nunca, jamás uses IPs fijas en tu código. Las IPs de los contenedores cambian al reiniciarse.
- Usa redes separadas. El DNS de Docker respeta el aislamiento: un contenedor en la red A no puede resolver nombres de la red B. Esto es seguridad por diseño.

## CIERRE (30 s)
Dominar el DNS interno te permitirá diseñar arquitecturas de micro‑servicios robustas. Tu código se vuelve más limpio y portable. ¡A practicar la resolución de nombres en los ejercicios!

## NOTAS DE PRODUCCIÓN
- Insertar pausa de 1 s después de cada sección.
- Enfatizar "Balanceo de carga gratis".
