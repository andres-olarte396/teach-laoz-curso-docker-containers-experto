# Contenido del Subtema 1 – Límites de CPU y Memoria

## Objetivo

Al finalizar este subtema, serás capaz de:

1.  Evitar que un solo contenedor con errores congele todo tu servidor.
2.  Entender el misterioso **Código de Error 137** (OOMKilled).
3.  Asignar cuotas justas de RAM y CPU a tus aplicaciones.

## Contenido Teórico

### El Problema: El Buffet Libre

Por defecto, Docker es un padre muy permisivo. Le dice a los contenedores:
*"Tomen toda la RAM y toda la CPU que quieran"*.

Esto es peligroso.
Imagina que tienes una aplicación Java con una fuga de memoria (Memory Leak). Empezará a tragar RAM... 1GB... 4GB... 16GB...
Cuando se acabe la RAM física, tu servidor entero se volverá lento y finalmente **colapsará**. Todas las demás aplicaciones morirán.

### 1. Límites de Memoria (RAM)

Podemos ponerle un tope a cada contenedor.
*   Comando: `--memory="512m"`
*   Compose: `deploy.resources.limits.memory: 512M`

**¿Qué pasa si el contenedor intenta comer más de 512MB?**
Aquí entra el villano de la película: **El OOM Killer (Out Of Memory Killer)**.

Es un mecanismo del Kernel de Linux (el jefe del sistema). Su trabajo es salvar el servidor a toda costa.
Si ve que un proceso (tu contenedor) violó su límite de memoria, **lo asesina instantáneamente**.
Sin aviso. Sin "guardar cambios". Un disparo a la cabeza.

*   **Síntoma**: Tu contenedor se reinicia solo o aparece en estado `Exited (137)`.
*   **Significado del 137**: 128 (Fatal Error) + 9 (Señal SIGKILL).

### 2. Límites de CPU

También podemos limitar la capacidad de procesamiento.
*   Comando: `--cpus="0.5"`
*   Significado: "Solo puedes usar la mitad de un núcleo".

A diferencia de la memoria, si un contenedor pide más CPU de la permitida, **NO se le mata**. Simplemente se le pone lento (Throttling). Docker lo frena.

### Configuración en Compose (Estándar Moderno)

```yaml
services:
  mi-app-pesada:
    image: java-app
    deploy:
      resources:
        limits:
          # Si pasas de esto, te mato
          memory: 1G
          # Si pasas de esto, te freno
          cpus: '0.50'
        reservations:
          # Garantizame al menos esto para arrancar
          memory: 256M
```

## Paso a Paso práctico

Vamos a provocar al OOM Killer.

1.  Busca una imagen diseñada para estresar el sistema, como `polinux/stress`.
2.  Lánzala con un límite ridículo (50MB) y pídele que consuma 100MB.
    ```bash
    docker run --rm --memory="50m" polinux/stress stress --vm 1 --vm-bytes 100M
    ```
3.  **Resultado inmediato**:
    `stress: FAIL: [1] <-- worker 8 got signal 9`
    El contenedor murió al instante.
4.  Verifica la autopsia:
    `docker inspect <id-contenedor> | grep OOMKilled`
    Verás: `"OOMKilled": true`.

## Resumen

*   Nunca confíes en tus aplicaciones. Ponles límites.
*   **Límite de Memoria**: Si se cruza, el contenedor **MUERE** (Error 137).
*   **Límite de CPU**: Si se cruza, el contenedor se **RALENTIZA**.
*   Usa `docker stats` para ver en vivo quién se está comiendo el buffet.
