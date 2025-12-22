# Guión de Audio – Pods y Nodos

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Pedagógico y Fundacional
- **Audiencia**: Arquitectos Cloud en formación

## INTRO (30 s)
Imagina un edificio de apartamentos. El edificio completo es el **Nodo**. Dentro de ese edificio, tienes apartamentos individuales, que son los **Pods**. Y dentro de cada apartamento, viven personas, que son los **Contenedores**. Bienvenidos a la arquitectura básica de Kubernetes.

## DESARROLLO (2 min)

### 1️⃣ El Nodo (Node)
- Antes conocido como "Minion" (sí, como los de la película). Es la máquina de trabajo.
- Puede ser una máquina virtual en AWS, un servidor físico en tu rack, o tu propia laptop.
- Kubernetes agrupa todos estos nodos en un gran "superordenador" abstracto. Tú no te preocupas por qué máquina ejecuta tu código; K8s lo decide por ti.

### 2️⃣ El Pod
- Aquí es donde muchos se confunden. "¿Por qué no ejecuto contenedores directamente?".
- Kubernetes necesita una capa extra para gestionar redes y volúmenes de forma inteligente. Esa capa es el Pod.
- Un Pod es un entorno estanco. Tiene su propia dirección IP.
- Normalmente, un Pod = Un Contenedor.
- Pero a veces, necesitas patrones avanzados, como un "sidecar" que envíe logs a la nube. En ese caso, metes dos contenedores en el mismo Pod. Compartirán la misma red y podrán hablarse como si estuvieran en la misma máquina local.

### 3️⃣ Vida y Muerte
- Los Pods son mortales. Efímeros.
- Si un Pod muere, Kubernetes no lo "arregla". Lo tira a la basura y crea uno nuevo, fresco y limpio, probablemente con una IP distinta.
- Por eso, nunca debes depender de la IP de un Pod. Son volátiles.

## CIERRE (30 s)
Recuerda: Contenedores dentro de Pods. Pods dentro de Nodos. Esa es la jerarquía sagrada. Practica creando y destruyendo Pods con `kubectl`. En el próximo tema, veremos cómo definirlos profesionalmente con YAML.

## NOTAS DE PRODUCCIÓN
- Usar la analogía del Edificio/Apartamento/Persona con claridad.
- Enfatizar "Nunca dependas de la IP de un Pod".
