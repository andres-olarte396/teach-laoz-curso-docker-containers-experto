# Evaluación – Tipos de Monturas

## Instrucciones
- Tiempo estimado: 10 minutos.
- Cada pregunta vale 10 puntos (total 60 puntos).

## Preguntas de Selección Múltiple (30 pts)

1. **¿Cuál es el tipo de almacenamiento recomendado para persistir datos de base de datos en producción?**
   a) Bind Mount.
   b) Volume. *(Correcta)*
   c) tmpfs.
   d) Layer del contenedor.

2. **¿Qué sucede si usas un `bind mount` para mapear el código fuente de tu host a un contenedor?**
   a) El contenedor recibe una copia estática del código al iniciarse.
   b) Los cambios en el host se reflejan inmediatamente en el contenedor. *(Correcta)*
   c) El contenedor borra el código del host al terminar.
   d) Es imposible hacer eso en Docker.

3. **¿Cuál es una ventaja clave de usar la sintaxis `--mount` sobre `-v`?**
   a) Es más corta de escribir.
   b) Es más explícita y valida que la ruta de origen exista en los bind mounts. *(Correcta)*
   c) Permite montar dispositivos USB automáticamente.
   d) No tiene ventajas, es solo estética.

## Preguntas de Desarrollo (30 pts)

4. **Explica la diferencia fundamental entre un `Volume` y un `Bind Mount` en términos de quién gestiona los archivos.**
   *Rúbrica*: 10 pts por indicar que en los **Volumes**, Docker gestiona los archivos en una ubicación interna y segura (`/var/lib/docker/volumes`), abstrayendo al usuario del sistema de archivos del host. En los **Bind Mounts**, el usuario gestiona directamente los archivos y su ubicación exacta en el host.

5. **Describe un escenario donde usarías una montura `tmpfs`.**
   *Rúbrica*: 10 pts por describir un caso de uso que requiera alta velocidad, seguridad (no escribir en disco) o volatilidad, como guardar claves de encriptación desencriptadas temporalmente o caches de sesión efímeras.

6. **Si eliminas un contenedor que usaba un Volumen, ¿qué pasa con los datos de ese volumen? Comparar con lo que pasa si no usas ninguna montura.**
   *Rúbrica*: 10 pts por explicar que si usas un Volumen, los datos **persisten** en el volumen y no se borran. Si no usas montura (capa de contenedor "writable layer"), los datos se **eliminan** permanentemente junto con el contenedor.
