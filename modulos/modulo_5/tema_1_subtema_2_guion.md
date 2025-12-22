# Guión de Audio – Usuario No-Root

## Metadata
- **Duración estimada**: 3 minutos
- **Tono**: Serio pero constructivo
- **Audiencia**: Devs listos para desplegar en producción real

## INTRO (30 s)
Docker tiene un "pecado original": por defecto, todo corre como **root**. Esto es cómodo para desarrollar, pero es una pesadilla de seguridad en producción. Si un hacker entra a tu contenedor, ¡prácticamente es dueño de tu servidor! Hoy vamos a cerrar esa puerta.

## DESARROLLO (2 min)

### 1️⃣ El Principio de Menor Privilegio
- Tu aplicación web no necesita permisos para instalar paquetes, formatear discos o cambiar la configuración de red.
- Solo necesita leer su código y escribir en `stdout`.
- Entonces, ¿por qué le damos permisos de superusuario? Es innecesario.

### 2️⃣ La Instrucción `USER`
- En tu Dockerfile, el remedio es simple.
- Primero, crea un usuario del sistema (con `adduser` o `useradd`).
- Segundo, usa la instrucción `USER <nombre>`.
- A partir de esa línea, todas las instrucciones (`RUN`, `CMD`) se ejecutan con ese usuario limitado.

### 3️⃣ Los Obstáculos Comunes
- **Puertos**: Un usuario normal no puede usar el puerto 80. Mueve tu app al 8080 o 3000.
- **Permisos de Archivos**: Si usas `COPY`, por defecto el dueño es root. Usa el flag `COPY --chown=usuario:grupo` para regalarle los archivos a tu nuevo usuario.
- **Volúmenes**: Asegúrate de que las carpetas montadas tengan permisos de escritura para el ID del usuario.

## CIERRE (30 s)
Correr como "no-root" es la medida de seguridad número uno que revisan los auditores. No esperes a que sea un requisito obligatorio. Hazlo parte de tu estándar hoy mismo con los ejercicios. ¡Tu infraestructura te lo agradecerá!

## NOTAS DE PRODUCCIÓN
- Tono de alarma en "¿Por qué le damos permisos de superusuario?".
- Explicar claro: "Si un hacker entra... es dueño de tu servidor".
