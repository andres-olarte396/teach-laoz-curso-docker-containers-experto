# Ejercicios: VMs vs Contenedores

## Nivel Básico (60-74%)

### Ejercicio 1. Comparación Directa
**Enunciado**: Completa la siguiente tabla indicando si la característica corresponde a una Máquina Virtual (VM) o a un Contenedor.

| Característica | ¿VM o Contenedor? |
| :--- | :--- |
| Tiene su propio Kernel independiente | |
| Arranca en milisegundos | |
| Utiliza un Hypervisor | |
| Pesa cientos de Megabytes (MB) | |
| Pesa Gigabytes (GB) | |

**Solución**:
```markdown
| Característica | ¿VM o Contenedor? |
| :--- | :--- |
| Tiene su propio Kernel independiente | VM |
| Arranca en milisegundos | Contenedor |
| Utiliza un Hypervisor | VM |
| Pesa cientos de Megabytes (MB) | Contenedor |
| Pesa Gigabytes (GB) | VM |
```

### Ejercicio 2: Identificando Componentes
**Enunciado**: En un diagrama de arquitectura de contenedores, ¿qué componente falta en la siguiente lista para que funcione docker en Linux?
1. Hardware
2. Host OS
3. ???
4. Contenedores (Binarios/Libs + App)

**Solución**:
```
Falta el "Container Engine" (o Docker Daemon/Engine). Es el responsable de comunicar los contenedores con el Kernel del Host OS.
```

## Nivel Intermedio (75-89%)

### Ejercicio 3: Análisis de Escenario
**Enunciado**: Una startup desea desplegar 50 microservicios diferentes. Tienen un presupuesto limitado para hardware.
1. Si usaran VMs para cada microservicio, ¿cuál sería el principal problema de recursos?
2. ¿Por qué el uso de contenedores ahorraría dinero en este caso?

**Solución**:
```
1. Problema de VMs: Cada microservicio requeriría un SO completo (Guest OS). Si cada SO consume 1GB de RAM solo para existir, necesitarían 50GB de RAM solo para los sistemas operativos, sin contar la memoria que necesitan las aplicaciones reales. Además del desperdicio de CPU en procesos "idle" del sistema.

2. Ahorro con Contenedores: Al compartir el mismo Kernel y OS Host, los 50 microservicios solo consumen la RAM que realmente necesitan para funcionar. El "overhead" (sobrecosto) es mínimo. Podrían correr los 50 servicios en una máquina mucho más pequeña, reduciendo costos de servidores/nube.
```

## Nivel Avanzado (90-100%)

### Ejercicio 4: Pensamiento Crítico - Seguridad
**Enunciado**: Si los contenedores son "mejores" en rendimiento, ¿por qué algunas industrias con regulaciones estrictas (banca, defensa) a veces prefieren seguir usando VMs o usan Contenedores DENTRO de VMs?
Pista: Piensa en el "Kernel compartido".

**Solución**:
```
El aislamiento de los contenedores es a nivel de software (namespaces/cgroups), compartiendo el mismo Kernel. Si un atacante logra un exploit de "Kernel Panic" o escapa del contenedor al Kernel (Container Breakout), podría comprometer todo el Host y todos los demás contenedores.

Las VMs ofrecen aislamiento por hardware (a través del Hypervisor). Si un kernel de una VM falla o es comprometido, el Hypervisor suele contener el daño a esa única VM. Por eso, para máxima seguridad ("Hard Multi-tenancy"), se suelen correr contenedores dentro de VMs aisladas.
```
