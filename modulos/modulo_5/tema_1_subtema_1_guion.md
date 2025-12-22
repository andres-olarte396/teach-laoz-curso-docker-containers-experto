# Guión de Audio – Seguridad del Docker Daemon

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Alerta y Serio
- **Audiencia**: Administradores de Sistemas y DevOps

## INTRO (30 s)
Docker es una herramienta poderosa, pero como dice el tío Ben: "Un gran poder conlleva una gran responsabilidad". El daemon de Docker es, esencialmente, root. Si no lo aseguras, estás dejando la puerta trasera de tu servidor abierta de par en par.

## DESARROLLO (2 min)

### 1️⃣ El Socket de La Muerte
- El archivo `/var/run/docker.sock` es la interfaz de control.
- Cualquiera que pueda hablar con este archivo puede decirle a Docker: "Monta todo el disco duro del servidor en este contenedor y borra el sistema operativo".
- **Nunca** montes este socket en contenedores de terceros o desconocidos. Solo en herramientas de confianza absoluta como Portainer o agentes de monitoreo, y aún así, ten cuidado.

### 2️⃣ Exposición en la Red
- A veces verás tutoriales que dicen: "Habilita el puerto 2375 para controlar Docker remotamente".
- **¡No lo hagas!** El puerto 2375 no tiene autenticación.
- Si necesitas acceso remoto, usa SSH (`docker context create --docker "host=ssh://usuario@servidor"`) o configura TLS mutuo en el puerto 2376.

### 3️⃣ User Namespaces
- Una defensa avanzada es el "User Remap".
- Hace que el `root` dentro del contenedor sea el usuario `nadie` (UID 65534) en el host.
- Así, incluso si escapan del contenedor, no tienen permisos de root en tu servidor real.

## CIERRE (30 s)
La seguridad empieza en la configuración. Revisa tu `daemon.json`, habilita `no-new-privileges` y trata al socket de Docker como si fuera la contraseña de root. ¡A auditar esos servidores!

## NOTAS DE PRODUCCIÓN
- Tono grave al mencionar "borra el sistema operativo".
- Enfatizar fuertemente "¡No lo hagas!".
