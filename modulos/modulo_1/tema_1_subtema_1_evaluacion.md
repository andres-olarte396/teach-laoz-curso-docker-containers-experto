# Evaluación: VMs vs Contenedores

## Instrucciones
- Tiempo estimado: 10 minutos
- Puntaje total: 20 puntos

---

## Selección Múltiple (5 puntos c/u)

### Pregunta 1
¿Cuál es la diferencia arquitectónica fundamental entre una VM y un Contenedor?
a) Las VMs usan Docker; los contenedores usan Kubernetes.
b) Las VMs virtualizan el hardware; los contenedores virtualizan el sistema operativo.
c) Las VMs son para Windows; los contenedores para Linux.
d) No hay diferencia, son nombres comerciales para lo mismo.

**Respuesta correcta**: b)
**Justificación**: La virtualización de hardware requiere un Hypervisor y un SO invitado completo. La containerización comparte el kernel del host.

### Pregunta 2
¿Qué elemento NO es necesario en una arquitectura de contenedores?
a) Host OS
b) Hypervisor
c) Container Engine
d) Hardware

**Respuesta correcta**: b)
**Justificación**: Los contenedores corren nativamente sobre el SO del host (o un SO ligero) sin necesidad de una capa de Hypervisor para emular hardware.

### Pregunta 3
Si tienes un servidor con 16GB de RAM y quieres correr aplicaciones que consumen 100MB cada una. ¿Por qué podrías correr MÁS instancias usando Docker que usando VMs?
a) Porque Docker comprime la memoria RAM.
b) Porque las VMs reservan memoria fija para el Sistema Operativo Invitado, desperdiciando recursos.
c) Porque Docker descarga RAM de la nube gratis.
d) Docker no permite correr más instancias, es un mito.

**Respuesta correcta**: b)
**Justificación**: El "overhead" de tener múltiples Kernels y procesos de sistema operativo en cada VM consume gran parte de la RAM disponible antes de que puedas siquiera correr tu aplicación.

### Pregunta 4
¿Qué significa que los contenedores sean "portátiles"?
a) Que solo corren en laptops.
b) Que puedes moverlos fisicamente en un USB.
c) Que una imagen creada en tu laptop correrá exactamente igual en un servidor de producción.
d) Que cambian de tamaño automáticamente.

**Respuesta correcta**: c)
**Justificación**: Al empaquetar todas las dependencias (librerías, configs) dentro de la imagen, se elimina el problema de "funciona en mi máquina". La portabilidad es una de las mayores ventajas de Docker.
