# Ejercicios – Conceptos de Cluster

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Single-Node Swarm**
1. Aunque solo tengas una computadora, puedes activar Swarm.
2. Ejecuta `docker swarm init`. (Si tienes múltiples IPs, usa `--advertise-addr` con tu IP principal).
3. Ejecuta `docker node ls`. Deberías ver tu nodo con un asterisco `*` indicando que es el líder activo.
4. Inspecciona tu nodo: `docker node inspect self --pretty`.

**Ejercicio 2 – Extrayendo Tokens**
1. Imagina que perdiste el token para unir workers.
2. Recuperalo con: `docker swarm join-token worker`.
3. Recupera el token para managers: `docker swarm join-token manager`.
4. Observa que son diferentes. Esto es vital para la seguridad.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Simulando Nodos (Play with Docker)**
*Nota: Si no tienes máquinas virtuales, usa [labs.play-with-docker.com](https://labs.play-with-docker.com/) o crea contenedores dind (docker-in-docker) localmente.*
1. Inicia 3 instancias "dind" o usa máquinas virtuales.
2. Inicializa el Swarm en el Nodo 1.
3. Une el Nodo 2 como Worker.
4. Une el Nodo 3 como Manager secundario.
5. Ejecuta `docker node ls` desde el Nodo 2. ¿Funciona? (Spoiler: No, los workers no tienen acceso a la API de gestión).

**Ejercicio 4 – Promoción y Dimisión**
1. Promueve el Nodo 2 a Manager: `docker node promote <ID-Nodo-2>`.
2. Ahora ejecuta `docker node ls` desde el Nodo 2. Debería funcionar.
3. Degrada el Nodo 2 a Worker de nuevo: `docker node demote <ID-Nodo-2>`.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Disponibilidad y Drenaje**
1. Marca tu nodo como "Drain" (Drenaje) para mantenimiento:
   `docker node update --availability drain <tu-nodo>`.
2. Si tuvieras contenedores corriendo, Swarm los movería a otro nodo. Como no tienes otros nodos reales (si estás en local), se quedarán en estado "Pending".
3. Vuelve a ponerlo en "Active": `docker node update --availability active <tu-nodo>`.

**Ejercicio 6 – Leaving the Swarm**
1. Para limpiar todo: `docker swarm leave --force`.
2. Verifica que `docker node ls` da error ("This node is not a swarm manager"), confirmando que volviste al modo estándar single-host.
