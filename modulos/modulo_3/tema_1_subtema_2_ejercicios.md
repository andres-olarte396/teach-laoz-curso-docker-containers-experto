# Ejercicios – DNS y Descubrimiento de Servicios

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Resolución de nombres**
1. Crea una red `testnet` y lanza dos contenedores (`db` usando `postgres` y `app` usando `nginx`).
2. Dentro del contenedor `app`, usa `ping db` (deberá instalarse `iputils-ping` si no está en la imagen) o `curl` para intentar acceder.
3. Observa que el nombre `db` resuelve automáticamente a la IP interna del contenedor de base de datos.

**Ejercicio 2 – Alias de red**
1. Repite el ejercicio anterior pero asigna un alias `database` al contenedor `db` usando `--network-alias`.
2. Verifica que `app` puede resolver tanto `db` como `database`.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Service Discovery en Swarm**
1. Inicializa un swarm (`docker swarm init`).
2. Crea una red overlay `app_overlay`.
3. Despliega un servicio `web` con 3 réplicas usando `nginx`.
4. Lanza un contenedor utilitario (ej. `alpine`) conectado a `app_overlay`.
5. Usa `nslookup web` (instala `bind-tools` en alpine) para ver cómo Docker resuelve la IP virtual del servicio.

**Ejercicio 4 – DNSRR vs VIP**
1. Modifica el servicio `web` para usar el modo `--endpoint-mode dnsrr`.
2. Observa la diferencia en la resolución DNS (deberías recibir una lista de IPs en lugar de una única VIP).

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Diagnóstico de problemas**
1. Intencionalmente desconecta un contenedor de la red (`docker network disconnect`).
2. Usa `docker exec` para intentar resolver el nombre del contenedor desconectado y describe el error "Name or service not known".
3. Luego reconecta y verifica que la resolución vuelve a funcionar.

**Ejercicio 6 – Seguridad del DNS interno**
1. Investiga cómo el DNS de Docker solo resuelve nombres de contenedores en la **misma** red.
2. Crea dos redes separadas y un contenedor en cada una.
3. Verifica que no pueden resolver sus nombres entre sí, demostrando el aislamiento de DNS.
