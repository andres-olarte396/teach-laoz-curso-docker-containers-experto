# PLAN CURRICULAR: Docker y Containers - De 0 a Experto

**Topic**: Docker y Containers: De 0 a Experto
**Complexity**: Alta
**Duration**: 40‑50 horas
**Audience**: Desarrolladores de Software

---

## 🗺️ Mapa de Dependencias

1. **Fundamentos (Mód 1)** → Base para todo.
2. **Construcción de Imágenes (Mód 2)** → Requiere Mód 1.
3. **Networking y Datos (Mód 3)** → Requiere Mód 2.
4. **Compose & Multi‑container (Mód 4)** → Requiere Mód 3.
5. **Producción & Seguridad (Mód 5)** → Requiere Mód 4.
6. **Orquestación Básica (Mód 6)** → Requiere Mód 5.

---

## 📚 Estructura de Módulos

### Módulo 1. Fundamentos de la Containerización

**Objetivo**: Comprender qué son los contenedores, diferencias con VMs y arquitectura de Docker.

- **1.1 Historia y Arquitectura**
  - VMs vs Contenedores
  - Arquitectura Docker Engine
- **1.2 Primeros Pasos**
  - Instalación y Hola Mundo
  - Ciclo de vida básico

### Módulo 2: Maestría en Imágenes (Dockerfiles)

**Objetivo**: Crear imágenes optimizadas, seguras y ligeras.

- **2.1 Dockerfiles Eficientes**
  - Instrucciones Clave
  - Contexto de Build
- **2.2 Optimización Avanzada**
  - Multi‑stage Builds
  - Gestión de Caché

### Módulo 3: Networking y Persistencia de Datos

**Objetivo**: Conectar contenedores y gestionar datos persistentes.

- **3.1 Redes en Docker**
  - Drivers de Red
  - DNS y Descubrimiento de Servicios
  - Configuración Avanzada de Redes
- **3.2 Volúmenes y Datos**
  - Tipos de Monturas
  - Backups y Migración

### Módulo 4: Orquestación Local con Docker Compose

**Objetivo**: Gestionar aplicaciones multi‑contenedor.

- **4.1 Aplicaciones Multi‑contenedor**
  - Docker Compose YAML
  - Dependencias y Healthchecks
- **4.2 Flujos de Desarrollo**
  - Development vs Production
  - Variables de Entorno

### Módulo 5: Seguridad y Buenas Prácticas en Producción

**Objetivo**: Hardening de contenedores para despliegue real.

- **5.1 Seguridad**
  - Seguridad del Docker Daemon
  - Usuario No‑Root
- **5.2 Recursos**
  - Límites de CPU y Memoria
  - Logging Drivers

### Módulo 6: Introducción a la Orquestación (Swarm/K8s)

**Objetivo**: Escalar más allá de un solo nodo.

- **6.1 Docker Swarm**
  - Conceptos de Cluster
  - Servicios y Escalamiento
- **6.2 Más allá de Docker**
  - Intro a Kubernetes

### Módulo 7: Fundamentos de Kubernetes

**Objetivo**: Entender la arquitectura y los objetos básicos de Kubernetes.

- **7.1 Arquitectura K8s**
  - Pods y Nodos
  - Manifiestos YAML
- **7.2 Orquestación K8s**
  - Deployments y ReplicaSets
  - Services y Networking

---

## 💾 Estructura JSON (Para Automatización)

```json
{
  "modulos": [
    {
      "id": 1,
      "titulo": "Fundamentos de la Containerización",
      "temas": [
        {
          "id": 1,
          "titulo": "Historia y Arquitectura",
          "subtemas": [
            { "id": 1, "titulo": "VMs vs Contenedores" },
            { "id": 2, "titulo": "Arquitectura Docker Engine" }
          ]
        },
        {
          "id": 2,
          "titulo": "Primeros Pasos",
          "subtemas": [
            { "id": 1, "titulo": "Instalación y Hola Mundo" },
            { "id": 2, "titulo": "Ciclo de vida básico" }
          ]
        }
      ]
    },
    {
      "id": 2,
      "titulo": "Maestría en Imágenes",
      "temas": [
        {
          "id": 1,
          "titulo": "Dockerfiles Eficientes",
          "subtemas": [
            { "id": 1, "titulo": "Instrucciones Clave" },
            { "id": 2, "titulo": "Contexto de Build" }
          ]
        },
        {
          "id": 2,
          "titulo": "Optimización Avanzada",
          "subtemas": [
            { "id": 1, "titulo": "Multi-stage Builds" },
            { "id": 2, "titulo": "Gestión de Caché" }
          ]
        }
      ]
    },
    {
      "id": 3,
      "titulo": "Networking y Persistencia",
      "temas": [
        {
          "id": 1,
          "titulo": "Redes en Docker",
          "subtemas": [
            { "id": 1, "titulo": "Drivers de Red" },
            { "id": 2, "titulo": "DNS y Descubrimiento de Servicios" },
            { "id": 3, "titulo": "Configuración Avanzada de Redes" }
          ]
        },
        {
          "id": 2,
          "titulo": "Volúmenes y Datos",
          "subtemas": [
            { "id": 1, "titulo": "Tipos de Monturas" },
            { "id": 2, "titulo": "Backups y Migración" }
          ]
        }
      ]
    },
    {
      "id": 4,
      "titulo": "Docker Compose",
      "temas": [
        {
          "id": 1,
          "titulo": "Aplicaciones Multi-contenedor",
          "subtemas": [
            { "id": 1, "titulo": "Docker Compose YAML" },
            { "id": 2, "titulo": "Dependencias y Healthchecks" }
          ]
        },
        {
          "id": 2,
          "titulo": "Flujos de Desarrollo",
          "subtemas": [
            { "id": 1, "titulo": "Development vs Production" },
            { "id": 2, "titulo": "Variables de Entorno" }
          ]
        }
      ]
    },
    {
      "id": 5,
      "titulo": "Seguridad y Producción",
      "temas": [
        {
          "id": 1,
          "titulo": "Seguridad",
          "subtemas": [
            { "id": 1, "titulo": "Seguridad del Docker Daemon" },
            { "id": 2, "titulo": "Usuario No-Root" }
          ]
        },
        {
          "id": 2,
          "titulo": "Recursos",
          "subtemas": [
            { "id": 1, "titulo": "Límites de CPU y Memoria" },
            { "id": 2, "titulo": "Logging Drivers" }
          ]
        }
      ]
    },
    {
      "id": 6,
      "titulo": "Orquestación",
      "temas": [
        {
          "id": 1,
          "titulo": "Docker Swarm",
          "subtemas": [
            { "id": 1, "titulo": "Conceptos de Cluster" },
            { "id": 2, "titulo": "Servicios y Escalamiento" }
          ]
        },
        {
          "id": 2,
          "titulo": "Más allá de Docker",
          "subtemas": [{ "id": 1, "titulo": "Intro a Kubernetes" }]
        }
      ]
    },
    {
      "id": 7,
      "titulo": "Fundamentos de Kubernetes",
      "temas": [
        {
          "id": 1,
          "titulo": "Arquitectura K8s",
          "subtemas": [
            { "id": 1, "titulo": "Pods y Nodos" },
            { "id": 2, "titulo": "Manifiestos YAML" }
          ]
        },
        {
          "id": 2,
          "titulo": "Orquestación K8s",
          "subtemas": [
            { "id": 1, "titulo": "Deployments y ReplicaSets" },
            { "id": 2, "titulo": "Services y Networking" }
          ]
        }
      ]
    }
  ]
}
```

---

_Este documento sirve como guía para la generación automática del curso y para la navegación del estudiante._
