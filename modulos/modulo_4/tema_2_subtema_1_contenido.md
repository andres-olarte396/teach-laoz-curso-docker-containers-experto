# Contenido del Subtema 1 – Development vs Production

## Objetivo

Al finalizar este subtema, serás capaz de:

1.  Tener un solo proyecto Docker que funcione "Relajado" en tu laptop y "Blindado" en el servidor.
2.  Usar la técnica de **Herencia (Merge)** para no repetir código.
3.  Entender la magia del archivo `docker-compose.override.yml`.

## Contenido Teórico

### El Dilema: Comodidad vs Seguridad

En **Desarrollo (Tu Laptop)** quieres:
*   Editar código y verlo al instante (Hot Reload).
*   Ver errores detallados en pantalla.
*   Usar contraseñas simples ("1234").

En **Producción (El Servidor)** quieres:
*   Código congelado e inmutable (Seguridad).
*   Si la app falla, que se reinicie sola (`restart: always`).
*   Contraseñas seguras y ocultas.

¿Cómo logramos esto sin tener dos archivos gigantes duplicados (`compose-dev.yml` y `compose-prod.yml`)?

---

### La Solución: El Sistema de Capas (Overrides)

Docker Compose permite sumar archivos. Piensa en esto como vestirse.
1.  **Archivo Base**: El cuerpo humano (Lo que es igual en todos lados).
2.  **Archivo Override**: La ropa que te pones según la ocasión.

#### 1. El Cuerpo (`docker-compose.yml`)
Aquí pones lo que NUNCA cambia: El nombre de los servicios y las imágenes base.

```yaml
services:
  web:
    image: mi-app
    networks:
      - red-interna
  db:
    image: postgres
```

#### 2. La Pijama (`docker-compose.override.yml`) - *Automático para Dev*
Docker busca este archivo automáticamente. Aquí pones las comodidades para trabajar en casa.

```yaml
services:
  web:
    # "En vez de usar la imagen, construye localmente"
    build: .
    # "Abre una ventana mágica para editar código"
    volumes:
      - ./src:/app/src
    # "Activa modo debug"
    environment:
      - DEBUG=true
```

#### 3. El Traje de Gala (`docker-compose.prod.yml`) - *Explícito para Prod*
Aquí pones la seguridad y robustez.

```yaml
services:
  web:
    # "Si te caes, levántate"
    restart: always
    # "Usa el puerto real 80"
    ports:
      - "80:80"
```

---

### ¿Cómo los ejecuto?

**En Desarrollo (Automático)**:
Solo escribe: `docker compose up`.
*   Docker detecta `docker-compose.yml` + `docker-compose.override.yml`.
*   Los fusiona y arranca.

**En Producción (Manual)**:
Tienes que decirle explícitamente qué ponerse:
`docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d`
*   Docker toma base + prod. (Ignora el override/pijama).

## El Truco del Mago: `docker compose config`

Si no estás seguro de cómo quedó la mezcla (¿se aplicó mi puerto? ¿se borró el volumen?), usa este comando:

```bash
docker compose config
```

Esto no arranca nada. Solo imprime en pantalla el YAML final resultante de la fusión. Es tu herramienta de diagnóstico #1.

## Resumen

*   **No repitas código**. Pone lo común en el base.
*   **Override** es tu amigo silencioso en desarrollo.
*   Usa el patrón de múltiples archivos (`-f`) para adaptar tu infraestructura como si cambiaras de ropa.
