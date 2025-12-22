# Guión de Audio – Intro a Kubernetes

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Épico y Conclusivo
- **Audiencia**: Graduados del Curso Docker

## INTRO (30 s)
¡Felicidades! Has dominado Docker, Compose y Swarm. Pero en el horizonte se alza un gigante. El sistema que maneja Google, Netflix y los bancos más grandes del mundo. Hablamos de **Kubernetes**, también conocido como K8s.

## DESARROLLO (2 min)

### 1️⃣ ¿Por qué Kubernetes?
- Docker Swarm es fantástico por su simplicidad. Pero Kubernetes es el **Estándar Universal**.
- K8s no solo maneja contenedores; maneja volúmenes, secretos, configuraciones, balanceadores de carga, certificados y políticas de red con un nivel de detalle granular.
- Es más complejo de aprender, sí. Pero te da un control absoluto.

### 2️⃣ El cambio de mentalidad: Pods
- En Docker, la unidad es el contenedor.
- En K8s, la unidad es el **Pod**. Un Pod es como una "cápsula" que envuelve a tu contenedor (o a varios contenedores que deben vivir y morir juntos).
- Tú no gestionas contenedores, gestionas Deployments que crean Pods.

### 3️⃣ Declarativo al 100%
- Si te gustó `docker-compose.yml`, amarás los manifiestos de K8s.
- Todo en K8s es un objeto descrito en YAML.
- Con el comando `kubectl apply -f archivo.yaml`, puedes desplegar infraestructuras enteras en segundos. Es la base de la filosofía GitOps.

## CIERRE (30 s)
Este curso te ha convertido en un experto en Docker. Ahora tienes los cimientos sólidos para dar el siguiente salto. Kubernetes no es más que la evolución lógica de lo que has aprendido aquí. ¡El mundo de la orquestación nativa de la nube te espera!

## NOTAS DE PRODUCCIÓN
- Música de fondo creciendo en intensidad hacia el final.
- Tono de "graduación" y "nuevos horizontes".
