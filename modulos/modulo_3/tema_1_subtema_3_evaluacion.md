# Evaluación – Configuración Avanzada de Redes

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es la principal característica del driver `macvlan`?**
   a) Asigna una dirección MAC única a cada contenedor, haciéndolos visibles directamente en la red física. *(Correcta)*
   b) Aísla completamente al contenedor de la red sin acceso a internet.
   c) Comparte la IP del host y usa puertos aleatorios.
   d) Crea una VPN automática entre hosts.

2. **¿Por qué podrías preferir `ipvlan` modo L2 sobre `macvlan`?**
   a) Porque permite usar DHCP.
   b) Porque los contenedores comparten la MAC address del host, evitando problemas con switches que tienen "Port Security" (límite de MACs por puerto). *(Correcta)*
   c) Porque es más lento pero más seguro.
   d) Porque funciona en Windows Home.

3. **Por defecto, ¿puede el host comunicarse directamente con un contenedor `macvlan` que corre sobre su propia interfaz física?**
   a) Sí, sin problemas.
   b) No, el kernel prohíbe esta comunicación directa por seguridad/arquitectura. *(Correcta)*
   c) Solo si el firewall está desactivado.
   d) Solo si usas IPv6.

## Preguntas de Desarrollo (30 pts)

4. **Describe un caso de uso real donde `bridge` no sea suficiente y necesites usar `macvlan`.**
   *Rúbrica*: 10 pts por mencionar un escenario como: Migración de aplicaciones monolíticas legacy que esperan tener su propia IP en la red corporativa, o necesidad de monitorear tráfico de red por IP individual desde el router central.

5. **Explica la diferencia entre `ipvlan L2` e `ipvlan L3`.**
   *Rúbrica*: 10 pts por explicar que L2 actúa como un switch (mismo segmento de red, broadcast funciona), mientras que L3 actúa como un router (sin broadcast, requiere enrutamiento estático en el gateway para llegar a los contenedores).

6. **¿Qué precaución debes tener al asignar un rango de IPs (`--ip-range`) a una red `macvlan`?**
   *Rúbrica*: 10 pts por explicar que el rango de IPs asignado a Docker debe estar reservado o excluido del servidor DHCP de la red local para evitar conflictos de IP duplicada con otros dispositivos físicos.
