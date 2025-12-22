# Guión de Audio – Configuración Avanzada de Redes

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Ingenieril y preciso
- **Audiencia**: Administradores de sistemas y redes

## INTRO (30 s)
A veces, el aislamiento de Docker es "demasiado bueno". Hay casos donde necesitas que tu contenedor sea un ciudadano de primera clase en tu red local, con su propia IP real. Para eso existen los pesos pesados: **macvlan** e **ipvlan**.

## DESARROLLO (2 min)

### 1️⃣ Macvlan: El Impostor
- Con el driver **macvlan**, Docker le asigna una dirección MAC virtual a tu contenedor.
- Tu switch y router ven al contenedor como si fuera un servidor físico conectado al cable.
- Puedes asignarle una IP de tu red corporativa (ej. 192.168.1.50).
- Úsalo cuando tengas aplicaciones antiguas que requieren estar en la misma subred que otros servidores físicos.

### 2️⃣ El "Gotcha" de Macvlan
- Advertencia: Por diseño de seguridad en Linux, **el host no puede hablar con sus propios contenedores macvlan**. El tráfico sale de la tarjeta de red pero el switch no lo devuelve al mismo puerto.
- Si necesitas comunicación host-contenedor, requiere trucos de enrutamiento avanzados.

### 3️⃣ Ipvlan: La Alternativa Ligera
- **Ipvlan** funciona casi igual pero es más eficiente.
- En modo **L2**, todos los contenedores comparten la MAC del host. Esto es vital si tu administrador de red bloqueó el puerto de tu switch para aceptar solo una MAC (Port Security).
- En modo **L3**, funciona como un router, eliminando el tráfico de broadcast. Ideal para miles de contenedores.

## CIERRE (30 s)
Estos drivers son herramientas de precisión. No los uses por defecto. Úsalos cuando la red `bridge` se quede corta o tengas requisitos de red legacy estrictos. ¡A configurar esas interfaces!

## NOTAS DE PRODUCCIÓN
- Tono de advertencia serio en la sección de "El Gotcha".
- Explicar "Port Security" como un problema común en empresas.
