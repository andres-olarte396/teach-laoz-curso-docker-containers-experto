# Evaluación – Límites de CPU y Memoria

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Qué sucede si un contenedor supera su límite estricto de memoria (`--memory`)?**
   a) Docker le asigna más memoria del swap automáticamente.
   b) El contenedor se pausa hasta que se libere RAM.
   c) El núcleo del sistema lo termina abruptamente (OOM Kill). *(Correcta)*
   d) Docker le envía un email al administrador.

2. **¿Qué significa el flag `--cpus="1.5"`?**
   a) Que el contenedor solo puede correr en un procesador Intel i5.
   b) Que el contenedor tiene garantizado el uso de 1.5 núcleos de CPU como máximo en cada periodo. *(Correcta)*
   c) Que usará 1 núcleo y medio gigabyte de RAM.
   d) Que tiene prioridad 1.5 sobre los demás.

3. **¿Cuál comando te permite ver el consumo de recursos en tiempo real de todos tus contenedores activos?**
   a) `docker top`
   b) `docker ps`
   c) `docker info`
   d) `docker stats` *(Correcta)*

## Preguntas de Desarrollo (30 pts)

4. **Explica por qué es peligroso no definir límites de memoria en un entorno multi-tenancy (varias apps en un mismo servidor).**
   *Rúbrica*: 10 pts por explicar que un solo contenedor con un memory leak o bajo ataque podría consumir el 100% de la RAM disponible, provocando que el sistema operativo se vuelva inestable y afecte o detenga a todos los demás servicios alojados en el mismo nodo (efecto "vecino ruidoso").

5. **¿Qué es el "Swappiness" en el contexto de Docker y memoria?**
   *Rúbrica*: 10 pts por explicar que controla la tendencia del kernel a mover memoria de este contenedor al disco (swap) antes de llegar al límite de RAM. Un valor bajo (0) prefiere matar el proceso antes que swappear (para evitar lentitud extrema), mientras que un valor alto permite swappear agresivamente.

6. **En un archivo `docker-compose.yml`, escribe la estructura YAML necesaria para limitar un servicio a 512MB de RAM y 1 CPU.**
   *Rúbrica*: 10 pts por:
   ```yaml
   deploy:
     resources:
       limits:
         cpus: '1'
         memory: 512M
   ```
