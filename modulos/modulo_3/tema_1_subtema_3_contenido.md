# Contenido del Subtema 3 – Configuración Avanzada de Redes

## Objetivo

Al finalizar este subtema, serás capaz de:

1.  Hacer que tus contenedores parezcan dispositivos físicos reales en tu red local.
2.  Entender la diferencia entre **macvlan** e **ipvlan**.
3.  Saber cuándo usar estas técnicas avanzadas (generalmente para migraciones Legacy).

## Contenido Teórico

### Introducción: Rompiendo la Cortina de Docker

Hasta ahora, usamos redes `NAT` (Bridge). Tus contenedores están ocultos detrás de la IP de tu servidor.
Pero, ¿qué pasa si tienes una aplicación vieja que exige tener su propia dirección IP en la red de la oficina (ej. `192.168.1.50`)?
Aquí entran los drivers avanzados.

### 1️⃣ macvlan: El Impostor Perfecto

Con `macvlan`, Docker le asigna una dirección MAC (hardware virtual) a cada contenedor.
**Efecto**: Tu Router Wi-Fi cree que has conectado una computadora física nueva.

*   **Uso**: Aplicaciones Legacy que monitorean tráfico de red o protocolos raros.
*   **Requisito**: ¡Tu tarjeta de red debe soportar "promiscuous mode"! (En la nube a veces está bloqueado).
*   **Limitation "Padre-Hijo"**: Por diseño de seguridad de Linux, **tu computadora (Host) NO puede hablar con los contenedores macvlan que hospeda**. Tienes que acceder a ellos desde otra máquina de la red.

### 2️⃣ ipvlan: El Hermano Eficiente

Es una versión moderna y ligera de macvlan.
*   **Modo L2 (Capa 2)**: Todos los contenedores comparten la misma dirección MAC del Host, pero tienen IPs distintas.
    *   *¿Para qué sirve?*: Algunos switches de oficina bloquean el puerto si ven muchas MAC addresses distintas saliendo del mismo cable. IPvlan L2 engaña al switch.
*   **Modo L3 (Capa 3)**: Funciona como un Router. Sin broadcast. Para redes gigantescas.

### 3️⃣ Comparativa Rápida

| Escenario | Driver Recomendado |
| :--- | :--- |
| **Normal** (Webs, APIs, DBs) | `bridge` (99% de los casos) |
| **Quiero que mi contenedor tenga IP 192.168.1.X** | `macvlan` |
| **Mi switch corporativo bloquea MACs nuevas** | `ipvlan` (Modo L2) |
| **Alto rendimiento sin NAT** | `host` |

## Configuración Práctica (Macvlan)

⚠️ *Nota: Esto no funciona bien en Docker Desktop (Windows/Mac) porque corren dentro de una VM oculta. Funciona mejor en Linux nativo.*

```bash
# 1. Crear la red conectada a tu tarjeta física (eth0)
# Asignamos un rango de IPs que tu Router NO esté usando (ej. .192 a .200)
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  --ip-range=192.168.1.192/29 \
  -o parent=eth0 macvlan_net

# 2. Crear contenedor con IP fija
docker run -d --network macvlan_net --ip 192.168.1.193 nginx
```

Si haces `ping 192.168.1.193` desde **otra** computadora de la red, responderá como si fuera un servidor real.

## Resumen

*   Usa **macvlan** para simular máquinas físicas.
*   Recuerda la regla de oro: El Host no ve a sus contenedores macvlan.
*   Si estás dudando, usa **bridge**. Solo usa esto si la red corporativa te obliga.
