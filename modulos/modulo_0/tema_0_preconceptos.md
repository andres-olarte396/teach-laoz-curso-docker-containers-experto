# Módulo 0: Conceptos Fundamentales y Glosario

## Propósito

Este módulo de nivelación asegura que todos los participantes tengan el mismo entendimiento base sobre sistemas operativos y virtualización antes de comenzar con Docker.

## Glosario Técnico

### Virtualización

**Definición**: Creación de una versión virtual (no real) de algo, como un sistema operativo, un servidor, un dispositivo de almacenamiento o un recurso de red.
**Contexto**: Antes de los contenedores, las máquinas virtuales (VMs) eran el estándar para el aislamiento de aplicaciones.

### Kernel

**Definición**: El núcleo de un sistema operativo. Es la capa que conecta el software con el hardware.
**Contexto**: Docker utiliza el kernel del sistema operativo host (en Linux) para ejecutar contenedores, lo que los hace más ligeros que las VMs.

### Shell / CLI

**Definición**: Interfaz de línea de comandos. Métodos para dar instrucciones a la computadora mediante texto.
**Contexto**: Docker se administra principalmente a través de la CLI (`docker run`, `docker ps`, etc.).

### Imagen (Image)

**Definición**: Un paquete ejecutable ligero e independiente que incluye todo lo necesario para ejecutar una pieza de software, incluido el código, el tiempo de ejecución, las herramientas del sistema, las bibliotecas y la configuración.
**Analogía**: Es como un "molde" o "plano" de una casa.

### Contenedor (Container)

**Definición**: Una instancia en ejecución de una imagen.
**Analogía**: Es la "casa" construida a partir del plano. Puedes construir muchas casas idénticas (contenedores) del mismo plano (imagen).

### Daemon

**Definición**: Un programa informático que se ejecuta como un proceso en segundo plano, en lugar de estar bajo el control directo de un usuario interactivo.
**Contexto**: El `dockerd` (Docker Daemon) es el proceso que gestiona los objetos de Docker como imágenes, contenedores, redes y volúmenes.

### Host

**Definición**: La máquina física o virtual donde se ejecuta el Docker Daemon.

## Conceptos Previos Necesarios

### 1. Navegación en Terminal

Docker se maneja principalmente desde la terminal. Debes sentirte cómodo con comandos básicos:

- **`ls` (List)**: Muestra los archivos en tu carpeta actual.
- **`cd` (Change Directory)**: Te mueve a otra carpeta (ej. `cd mis-proyectos`).
- **`mkdir` (Make Directory)**: Crea una carpeta nueva.
- **`pwd` (Print Working Directory)**: Te dice dónde estás parado ahora mismo.

### 2. Permisos de Archivos

En Linux (y dentro de los contenedores), cada archivo tiene un sistema de control de acceso:

- **Lectura (Read - r)**: Ver el contenido.
- **Escritura (Write - w)**: Modificar el archivo.
- **Ejecución (Execute - x)**: Correr el archivo como un programa.
  _¿Por qué importa?_ A veces un contenedor fallará porque no tiene permiso para escribir en una carpeta que compartiste.

### 3. Puertos de Red

Imagina tu computadora como un edificio de apartamentos (Dirección IP). Cada apartamento es un **Puerto**.

- **IP**: La dirección de la máquina (ej. `192.168.1.5` o `127.0.0.1` para localhost).
- **Puerto**: Un número del 1 al 65535 donde un servicio específico escucha. - Puerto 80: Web normal (HTTP). - Puerto 443: Web segura (HTTPS). - Puerto 3306: MySQL.
  _Tip_: En Docker, "mapear puertos" significa conectar un puerto de tu máquina real (Host) con un puerto dentro del contenedor.

### 4. Variables de Entorno

Son configuraciones que viven en el sistema operativo, fuera de tu código, en formato `CLAVE=VALOR`.

- **Ejemplo**: `DATABASE_URL=postgres://usuario:pass@localhost:5432/db`
- **Uso**: Las aplicaciones modernas (12-Factor App) leen su configuración de estas variables.
- **En Docker**: Usamos variables de entorno intensivamente para configurar contenedores sin tocar su código fuente.

## Tabla de Conceptos Clave de Docker

| Concepto               | Definición                                                                                                                     | Contexto o Aplicación                                                                                                           | Analogía o Ejemplo                                                                            | Categoría            | Fuente |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | -------------------- | ------ |
| Contenedor (Container) | Una instancia en ejecución de una imagen.                                                                                      | Es el proceso aislado donde se ejecuta la aplicación dentro del ecosistema Docker.                                              | Es la "casa" construida a partir del plano (imagen).                                          | Contenedores         | 1      |
| Imagen (Image)         | Paquete ejecutable ligero e independiente que incluye código, tiempo de ejecución, herramientas, bibliotecas y configuración.  | Es el archivo estático que sirve como base para crear contenedores de Docker.                                                   | Es como un "molde" o "plano" de una casa.                                                     | Contenedores         | 1      |
| Kernel                 | El núcleo de un sistema operativo; la capa que conecta el software con el hardware.                                            | Docker utiliza el kernel del sistema operativo host (en Linux) para ejecutar contenedores, haciéndolos más ligeros que las VMs. | No disponible en la fuente                                                                    | Sistema Operativo    | 1      |
| Shell / CLI            | Interfaz de línea de comandos para dar instrucciones a la computadora mediante texto.                                          | Docker se administra principalmente a través de la CLI mediante comandos como `docker run` o `docker ps`.                       | No disponible en la fuente                                                                    | Comandos de Terminal | 1      |
| Daemon                 | Un programa que se ejecuta como un proceso en segundo plano sin control directo del usuario.                                   | El `dockerd` (Docker Daemon) es el proceso que gestiona los objetos de Docker como imágenes, contenedores y redes.              | No disponible en la fuente                                                                    | Sistema Operativo    | 1      |
| Puertos de Red         | Un número del 1 al 65535 donde un servicio específico escucha tráfico.                                                         | En Docker, se mapean puertos para conectar un puerto de la máquina host con un puerto dentro del contenedor.                    | Imagina tu computadora como un edificio de apartamentos (IP) y cada apartamento es un puerto. | Redes                | 1      |
| Variables de Entorno   | Configuraciones en formato CLAVE=VALOR que viven en el sistema operativo fuera del código.                                     | Se usan intensivamente en Docker para configurar contenedores sin necesidad de modificar el código fuente.                      | `DATABASE_URL=postgres://usuario:pass@localhost:5432/db`                                      | Sistema Operativo    | 1      |
| Virtualización         | Creación de una versión virtual (no real) de algo, como un sistema operativo, un servidor, un recurso de red o almacenamiento. | Antes de los contenedores, las máquinas virtuales eran el estándar para el aislamiento de aplicaciones.                         | No disponible en la fuente                                                                    | Virtualización       | 1      |
| Host                   | La máquina física o virtual donde se ejecuta el Docker Daemon.                                                                 | Es el entorno anfitrión que provee los recursos para que Docker funcione.                                                       | No disponible en la fuente                                                                    | Sistemas             | 1      |
| Permisos de Archivos   | Sistema de control de acceso (Lectura r, Escritura w, Ejecución x).                                                            | Importante porque un contenedor puede fallar si no tiene permisos para escribir en una carpeta compartida del host.             | No disponible en la fuente                                                                    | Sistema Operativo    | 1      |
