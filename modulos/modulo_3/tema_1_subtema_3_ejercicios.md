# Ejercicios – Configuración Avanzada de Redes

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Requisitos de Macvlan**
1. Ejecuta `ip addr` (o `ifconfig`) en tu host para identificar tu interfaz principal (ej. `eth0` o `enp3s0`).
2. Identifica el rango de IP y Gateway de tu red local.
3. Escribe el comando `docker network create` teórico para crear una red macvlan que use un rango pequeño de IPs libres (ej. `.200` a `.210`) de tu red local.

**Ejercicio 2 – Creación de Macvlan (Simulada)**
Si no puedes hacerlo en tu red real, usa una subred ficticia.
1. Crea la red `macvlan_test` :
   `docker network create -d macvlan --subnet=10.0.0.0/24 -o parent=eth0 mv_net`.
2. Inspecciona la red con `docker network inspect mv_net` y verifica el driver y las opciones.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Lanzar en Macvlan**
1. Lanza un contenedor `alpine` en la red `mv_net`:
   `docker run -it --rm --network mv_net alpine ip addr`.
2. Observa la interfaz `eth0` dentro del contenedor. ¿Tiene una MAC diferente a la de tu host?

**Ejercicio 4 – El problema de comunicación Host-Contenedor**
1. Con el contenedor anterior corriendo, intenta hacerle ping desde tu terminal del HOST.
2. Debería fallar (o no responder).
3. Explica brevemente por qué ocurre esto (seguridad del kernel Linux).

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Ipvlan L2**
1. Crea una red `ipvlan_l2` usando el mismo parent que antes.
2. Lanza dos contenedores en ella.
3. Verifica que pueden hablar entre ellos.
4. Verifica que comparten la MAC Address del host (o de la interfaz padre).

**Ejercicio 6 – Solución Host-Access (Teórico)**
Investiga y escribe los comandos necesarios para crear una interfaz `shim` en el host que permita la comunicación con contenedores macvlan.
(Pista: `ip link add link eth0 name macvlan0 type macvlan mode bridge`).
