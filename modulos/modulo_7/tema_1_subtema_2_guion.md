# Guión de Audio – Manifiestos YAML

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Profesional y Técnico
- **Audiencia**: Desarrolladores y SysAdmins

## INTRO (30 s)
¿Alguna vez has configurado un servidor manualmente y luego has olvidado qué comandos ejecutaste? Eso es el infierno de la infraestructura "Snowflake". Hoy aprenderemos a evitar eso. Bienvenidos al mundo de la **Infraestructura como Código** con los manifiestos YAML de Kubernetes.

## DESARROLLO (2 min)

### 1️⃣ Imperativo vs Declarativo
- Imagina que pides un taxi.
- Método Imperativo: "Gire a la derecha, frene, siga recto 100 metros, gire a la izquierda". Estás micro-gestionando.
- Método Declarativo: "Lléveme al Aeropuerto". Tú defines el destino (el estado deseado) y el taxista (Kubernetes) decide la ruta.
- En K8s, usamos archivos YAML para describir ese "destino".

### 2️⃣ La Estructura Sagrada
- Todo archivo K8s tiene 4 pilares. Memorízalos.
- **apiVersion**: El idioma que hablamos.
- **kind**: Qué objeto queremos (Pod, Service, etc.).
- **metadata**: Cómo se llama y cómo lo etiquetamos.
- **spec**: La especificación técnica. Aquí va la "carne": imagen, puertos, volúmenes.

### 3️⃣ Kubectl Apply
- Olvídate de `create`, `edit`, `patch`.
- En el día a día, usarás casi exclusivamente `kubectl apply -f tu-archivo.yaml`.
- Este comando es idempotente. Puedes ejecutarlo 100 veces. Si el estado ya es el correcto, no hará nada. Si algo cambió, solo "parcheará" la diferencia.
- Esto te permite guardar tus YAMLs en Git y tener un historial perfecto de tu infraestructura.

## CIERRE (30 s)
A partir de ahora, todo lo que hagas en el clúster debe estar escrito en un archivo YAML. Si no está en el archivo, no existe. Esa es la disciplina que distingue a un aficionado de un experto en Kubernetes. ¡A escribir código!

## NOTAS DE PRODUCCIÓN
- Tono firme al decir "Si no está en el archivo, no existe".
- Pronunciar YAML como "Yamel".
