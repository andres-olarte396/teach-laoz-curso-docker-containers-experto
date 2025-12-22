# Contenido del Subtema 2 – Servicios y Escalamiento

## Objetivo

Al finalizar este subtema, serás capaz de:

1.  Escalar tu aplicación de 1 a 1000 copias con un solo comando.
2.  Dejar de tratar a tus servidores como **Mascotas** y empezar a tratarlos como **Ganado**.
3.  Actualizar tu aplicación sin que los usuarios noten ni un milisegundo de caída.

## Contenido Teórico

### El Cambio de Mentalidad: Mascotas vs Ganado

- **Mundo Viejo (`docker run`)**: Creas el contenedor "Servidor-Web-Principal". Si se cae, corres en círculos gritando y tratas de revivirlo manualmente. Es tu mascota, le tienes cariño.
- **Mundo Nuevo (`docker service`)**: Dices "Necesito 5 servidores web funcionando". No te importa cómo se llaman ni dónde están. Si uno muere, Swarm crea otro idéntico al instante. Es ganado.

### El Servicio (Service)

Un **Servicio** es la definición del estado que deseas.
Es un contrato que firmas con Docker Swarm:
_"Prometo mantener siempre 3 réplicas de Nginx vivas"_.

Swarm monitorea el sistema cada segundo.

- ¿Hay 3 réplicas? -> Todo bien.
- ¿Hay 2 réplicas (alguien mató una)? -> **¡ALARMA! Crea una nueva ya.**

### Escalamiento Trivial

¿Tu sitio web se hizo viral? En el pasado, esto era pánico.
En Swarm:

```bash
docker service scale mi-web=50
```

Listo. En segundos tienes 50 réplicas atendiendo tráfico.
¿Pasó la viralidad?

```bash
docker service scale mi-web=5
```

Ahorras recursos.

### Actualizaciones sin Caída (Rolling Updates)

Imagina que quieres pasar de la versión `v1` a la `v2`.
En el pasado: "Sitio en Mantenimiento" (Apagabas todo, subías lo nuevo, prendías).

En Swarm:

```bash
docker service update --image mi-web:v2 mi-web
```

Swarm hará esto:

1.  Apaga la Réplica #1 (v1).
2.  Enciende la Réplica #1 (v2). Espera a que esté verde (Healthy).
3.  Si funciona, pasa a la Réplica #2.
4.  Si falla, **se detiene y vuelve atrás automáticamente (Rollback)**.

¡Tus usuarios nunca ven un error 500!

## Paso a Paso práctico

1.  **Crear el Servicio**:
    ```bash
    docker service create --name web --replicas 2 -p 8080:80 nginx:alpine
    ```
2.  **Ver el estado**:
    `docker service ps web` (Verás 2 tareas corriendo).
3.  **El Sabotaje**:
    Borra manualmente un contenedor (¡ojo, un contenedor, no el servicio!).
    `docker rm -f <id-contenedor>`
4.  **La Magia**:
    Vuelve a ejecutar `docker service ps web`.
    Verás que Swarm detectó el crimen y creó una nueva réplica inmediatamente para cumplir el contrato de 2.

## Resumen

- **Servicio**: El jefe que manda.
- **Tarea (Task)**: El contenedor que trabaja.
- **Escalar**: Es cambiar un número en el contrato.
- **Update**: Es cambiar las ruedas del auto mientras sigue andando.
