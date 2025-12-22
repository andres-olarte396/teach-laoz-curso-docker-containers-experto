# Ejercicios – Límites de CPU y Memoria

## Nivel Básico (≈ 5 min)

**Ejercicio 1 – Limitando RAM**
1. Lanza un contenedor `nginx` con un límite de memoria ridículamente bajo (ej. 4MB).
   `docker run -d --name memtest --memory="4m" nginx`
2. Verifica si arrancó (`docker ps -a`). Probablemente falló o murió enseguida porque Nginx necesita más.
3. Repite con 64MB. Ahora debería vivir.

**Ejercicio 2 – Observando `docker stats`**
1. Lanza 3 contenedores cualquiera.
2. Ejecuta `docker stats`.
3. Observa las columnas `MEM USAGE / LIMIT` y `CPU %`.
4. Familiarízate con la visualización en tiempo real.

## Nivel Intermedio (≈ 10 min)

**Ejercicio 3 – Provocando un OOM Kill**
1. Usa la imagen `polinux/stress` para estresar la memoria.
   ```bash
   docker run --rm --memory="100m" polinux/stress stress --vm 1 --vm-bytes 150M
   ```
2. El contenedor debería morir casi al instante.
3. Observa el mensaje de salida o usa `docker inspect` en el ID del contenedor (si no usaste `--rm`) para confirmar la causa.

**Ejercicio 4 – Limitando CPU**
1. Lanza el estresador de CPU sin límites (cuidado si tu PC es lenta):
   `docker run --rm -d --name cpu_full polinux/stress stress --cpu 4`
2. Mira `docker stats`. Debería consumir cerca del 100% de los cores asignados (o 400% si tienes 4 cores).
3. Mátalo.
4. Lanza de nuevo limitado a medio core:
   `docker run --rm -d --name cpu_half --cpus="0.5" polinux/stress stress --cpu 4`
5. Mira `docker stats`. No debería pasar del 50%.

## Nivel Avanzado (≈ 15 min)

**Ejercicio 5 – Configuración en Compose v3**
1. Crea un `docker-compose.yml` con un servicio `stress`.
2. Define los límites usando la sintaxis `deploy.resources.limits`.
   ```yaml
   deploy:
     resources:
       limits:
         cpus: '0.50'
         memory: 50M
   ```
3. Ejecuta con `docker compose up`.
4. Nota: En versiones antiguas de Compose (v2 file format), esto se ignoraba si no estabas en modo Swarm. En Compose v2 (plugin), la especificación Compose Specification lo soporta nativamente. Verifica si funciona en tu versión (`docker compose version`). Si no, usa el flag `--compatibility`.

**Ejercicio 6 – Java Heap vs Container Limit**
1. (Teórico/Investigación) Si le das 512MB al contenedor, pero tu aplicación Java (JVM) intenta reservar 1GB de Heap, ¿qué pasa?
2. Investiga los flags `-XX:MaxRAMPercentage` en Java modernos que hacen que la JVM respete el límite de Docker automáticamente.
