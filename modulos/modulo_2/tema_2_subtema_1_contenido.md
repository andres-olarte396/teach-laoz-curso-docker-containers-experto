# Contenido del Subtema 1 – Multi‑stage Builds

## Objetivo

Al finalizar este subtema, serás capaz de:

1.  Crear imágenes minúsculas y profesionales (de 1GB a 20MB).
2.  Entender el patrón de **Construcción en Etapas** (Multi-stage).
3.  Escribir Dockerfiles que primero compilan (ensucian) y luego empaquetan (limpian).

## Contenido Teórico

### El Problema: El Cohete Pesado

Imagina que para enviar a 3 astronautas a la Luna (tu aplicación), envías también todo el cohete gigante de 100 metros, los tanques de combustible vacíos y a los ingenieros que lo construyeron. ¡Es absurdo!

Tradicionalmente, en Docker pasaba eso:
1.  Instalabas el compilador de Java (JDK) -> 300MB.
2.  Instalabas Maven/Gradle -> 100MB.
3.  Copiabas todo tu código fuente -> 50MB.
4.  Compilabas tu app -> Salía un archivo `.jar` de 5MB.

**Resultado Final**: Una imagen de **500MB** para correr un archivo de **5MB**.

---

### La Solución: Multi-stage Builds (El Cohete por Etapas)

Docker permite usar múltiples instrucciones `FROM` en el mismo archivo. Funciona como un cohete espacial:

**Etapa 1: El Constructor (El Cohete Impulsor)**
*   Usa una imagen base pesada y completa (`golang`, `node`, `maven`).
*   Compila el código.
*   Genera el ejecutable (el artefacto).
*   *Destino*: Se desecha al final.

**Etapa 2: El Ejecutor (La Cápsula)**
*   Empieza desde cero con una imagen base minúscula (`alpine`).
*   **COPIA** solo el ejecutable de la Etapa 1.
*   *Destino*: Es la imagen final que va a producción.

### Anatomía de un Dockerfile Multi-stage

Veamos un ejemplo real con el lenguaje Go (famoso por generar binarios pequeños):

```dockerfile
# --- ETAPA 1: EL SUCIO ---
# Le ponemos un alias "builder" para llamarlo después
FROM golang:1.21 AS builder

# Hacemos todo el trabajo sucio aquí
WORKDIR /app
COPY . .
RUN go build -o mi-super-app main.go
# Aquí tenemos una imagen que pesa 800MB...

# --- ETAPA 2: EL LIMPIO ---
# Empezamos de nuevo. Reset total.
FROM alpine:latest

WORKDIR /root/

# ¡LA MAGIA!
# "Oye, ve a la etapa 'builder' y róbale solo el archivo '/app/mi-super-app'"
COPY --from=builder /app/mi-super-app .

# Comando final
CMD ["./mi-super-app"]
```

**Resultado Real**: Una imagen de **10MB**. (5MB de Alpine + 5MB de tu App). ¡Redujiste el tamaño en un 98%!

### Beneficios Clave
1.  **Ahorro de Dinero**: Menos espacio en disco y transferencias de red más rápidas (bajar 10MB vs 800MB).
2.  **Seguridad Extrema**: En tu imagen final NO hay código fuente, ni herramientas de compilación que un hacker podría usar. Solo está el binario final.
3.  **Comodidad**: No necesitas instalar Go/Java/Node en tu computadora local. Docker lo compila por ti.

## Paso a Paso práctico

1.  **Observa**: Mira un Dockerfile "viejo" que instala compiladores y código fuente.
2.  **Refactoriza**: Divídelo en dos bloques `FROM`.
3.  **Copia**: Usa `COPY --from=0` (o usa alias `AS name`) para rescatar lo valioso.
4.  **Compara**: Usa `docker images` y sorpréndete con la diferencia de tamaño.

## Resumen

*   **`AS nombre`**: Dale un apodo a tu primera etapa.
*   **`COPY --from=nombre`**: La herramienta para rescatar archivos de la etapa anterior.
*   El objetivo es que los usuarios finales (producción) reciban solo lo necesario para ejecutar, no para construir.
