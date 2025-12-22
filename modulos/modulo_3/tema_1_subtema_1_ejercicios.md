# Ejercicios – Drivers de Red

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Identificación de drivers**
Enumera los cinco tipos de drivers de red que Docker ofrece y escribe una breve descripción (una frase) de cada uno.

**Ejercicio 2 – Creación de red bridge**
1. Crea una red bridge personalizada llamada `mi_red_app` con la subred `172.25.0.0/16`.
2. Verifica su creación con `docker network ls` y `docker network inspect mi_red_app`.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Comunicación entre contenedores**
1. Lanza un contenedor `alpine` llamado `c1` en la red `mi_red_app` que haga un loop infinito (`sleep infinity`).
2. Lanza otro contenedor `alpine` llamado `c2` en la misma red.
3. Desde `c2`, haz ping a `c1` (`ping -c 2 c1`).
4. Intenta hacer ping a `c1` desde un tercer contenedor que NO esté en esa red (usando la red default). ¿Funciona?

**Ejercicio 4 – Driver Host**
1. Ejecuta `docker run --rm -d --network host --name nginx_host nginx`.
2. Verifica en qué puerto está escuchando en tu máquina local. (Nota: Si usas Docker Desktop en Mac/Windows, el modo host tiene limitaciones, puede que necesites acceder a través de la IP de la VM).
3. Detén el contenedor.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Conectando a múltiples redes**
1. Crea una segunda red bridge `mi_red_admin`.
2. Conecta el contenedor `c1` (del ej 3) a `mi_red_admin` sin detenerlo (`docker network connect ...`).
3. Lanza un contenedor `admin` en `mi_red_admin`.
4. Verifica que `admin` puede ver a `c1`, pero `c2` (que solo está en `mi_red_app`) NO puede ver a `admin`.

**Ejercicio 6 – Macvlan (Teórico/Simulad)**
Diseña el comando para crear una red macvlan que asigne IPs del rango de tu red doméstica (ej. 192.168.1.0/24), excluyendo las primeras 10 IPs para no chocar con el router.
