# Guión de Audio – Drivers de Red

## Metadata
- **Duración estimada**: 4 minutos
- **Tono**: Técnico y claro
- **Audiencia**: Arquitectos y Devs conectando servicios

## INTRO (30 s)
Docker no es una isla... a menos que tú lo quieras. La red es la sangre de tus aplicaciones distribuidas. Hoy vamos a diseccionar los **Drivers de Red** para que sepas exactamente cómo fluyen tus paquetes.

## DESARROLLO (2 min)

### 1️⃣ El Estándar: Bridge
- Por defecto, Docker usa **Bridge**. Imagina un switch virtual dentro de tu computadora.
- Todos los contenedores conectados ahí pueden hablarse entre sí, pero están ocultos del mundo exterior (tu red Wi-Fi o LAN).
- Para salir, usan NAT.
- **Regla**: Siempre crea tus propias redes bridge (`docker network create`). Así tienes DNS automático: tus contenedores se llaman por nombre, "api" llama a "db", ¡magia!

### 2️⃣ Sin Barreras: Host
- El driver **Host** elimina el aislamiento.
- El contenedor comparte la tarjeta de red de tu servidor. Si la app escucha en el puerto 80, ocupa el puerto 80 de tu máquina.
- Es rapidísimo, pero peligroso: solo puede haber una app en el puerto 80.

### 3️⃣ Avanzados: None, Macvlan y Overlay
- **None**: Para paranoicos o procesos offline. Sin red.
- **Macvlan**: Le da al contenedor su propia MAC address. Tu router lo ve como un dispositivo físico más. Útil para apps legacy que exigen tener su propia IP real.
- **Overlay**: La joya de la corona para clusters. Conecta contenedores que están en servidores físicos diferentes. Es la base de Swarm y Kubernetes.

## CIERRE (30 s)
El 90% del tiempo usarás **Bridge**. El otro 10% usarás Host o Overlay cuando escales. Domina el comando `docker network create` y nunca más tendrás que pelear con IPs manuales. ¡A los ejercicios!

## NOTAS DE PRODUCCIÓN
- Insertar pausa de 1s entre cada driver.
- Enfatizar "DNS automático" con entusiasmo.
