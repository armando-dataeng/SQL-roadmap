# PROFILES

## Definición

Un Profile es un conjunto de políticas que controla los límites de recursos y las reglas de autenticación aplicadas a los usuarios de una base de datos.

Su objetivo es mejorar la seguridad, controlar el consumo de recursos y estandarizar la administración de usuarios.

---

# ¿Por qué existen?

Supongamos una empresa con:

```text
DBAs

Desarrolladores

Analistas

Aplicaciones

Procesos ETL
```

---

Pregunta:

```text
¿Todos los usuarios
deberían tener
las mismas reglas
de seguridad?
```

---

Respuesta:

```text
No.
```

---

Cada tipo de usuario requiere políticas diferentes.

La solución es:

```text
Profiles.
```

---

# Concepto Fundamental

Un Profile define reglas como:

```text
Tiempo máximo de sesión

Número de intentos fallidos

Complejidad de contraseñas

Tiempo de inactividad

Consumo de CPU

Consumo de memoria
```

---

Después se asigna a uno o varios usuarios.

---

# Arquitectura

```text
Usuario

↓

Profile

↓

Políticas

↓

Base de Datos
```

---

# ¿Qué puede controlar un Profile?

## Seguridad

Ejemplos:

```text
Longitud mínima
de contraseña

Expiración
de contraseña

Historial
de contraseñas

Intentos fallidos
```

---

## Recursos

Ejemplos:

```text
Tiempo de CPU

Tiempo de conexión

Sesiones simultáneas

Tiempo de inactividad
```

---

# Ejemplo (Oracle)

Crear un Profile:

```sql
CREATE PROFILE analyst_profile
LIMIT
    FAILED_LOGIN_ATTEMPTS 5
    PASSWORD_LIFE_TIME 90
    SESSIONS_PER_USER 2;
```

---

Asignarlo a un usuario:

```sql
ALTER USER analyst
PROFILE analyst_profile;
```

---

Resultado:

```text
Analyst

↓

Analyst Profile

↓

Reglas aplicadas
```

---

# Ejemplo de Políticas

## Contraseña

```text
Expira cada
90 días.
```

---

## Intentos Fallidos

```text
Máximo:

5
```

---

## Tiempo de Inactividad

```text
30 minutos.
```

---

## Sesiones

```text
2 simultáneas.
```

---

# Casos de Uso

## Analistas

```text
Solo horario laboral.

Sesiones limitadas.
```

---

## Aplicaciones

```text
Contraseña administrada.

Sin acceso interactivo.
```

---

## ETL

```text
Mayor tiempo
de ejecución.

Sesiones controladas.
```

---

## DBA

```text
Restricciones mínimas.

Auditoría reforzada.
```

---

# Beneficios

## Mayor seguridad

Políticas homogéneas.

---

## Administración sencilla

Cambios centralizados.

---

## Control de recursos

Evita abusos.

---

## Cumplimiento normativo

Facilita auditorías.

---

## Escalabilidad

Un Profile puede reutilizarse para muchos usuarios.

---

# DBMS y Profiles

## Oracle

Implementación completa.

---

## PostgreSQL

No tiene Profiles como Oracle.

Se utilizan:

```text
Roles

Parámetros

Configuraciones
```

---

## SQL Server

Utiliza:

```text
Logins

Roles

Resource Governor
```

---

## MySQL

Controla usuarios y permisos, pero no posee un sistema de Profiles equivalente al de Oracle.

---

# Buenas Prácticas

## Crear Profiles por tipo de usuario

Ejemplo:

```text
DBA

Developer

Analyst

Application

ETL
```

---

## Aplicar políticas de contraseñas

Mantener estándares de seguridad.

---

## Limitar sesiones

Evitar consumo excesivo.

---

## Revisar periódicamente

Actualizar políticas según las necesidades del negocio.

---

## Documentar cada Profile

Facilita mantenimiento y auditorías.

---

# Error Común

Crear todos los usuarios con:

```text
DEFAULT PROFILE
```

---

Resultado:

```text
Mismas reglas

para todos.

Menor seguridad.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Profile

=

Rol.
```

---

Incorrecto.

Un:

```text
Rol
```

controla:

```text
Permisos.
```

---

Un:

```text
Profile
```

controla:

```text
Políticas

de seguridad

y recursos.
```

---

# Comparación

| Concepto | Función |
|----------|---------|
| User | Identidad |
| Role | Permisos |
| Profile | Políticas de seguridad y recursos |

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia
entre un Role
y un Profile?
```

---

Respuesta:

```text
Un Role define qué acciones puede realizar un usuario dentro de la base de datos mediante permisos.

Un Profile define políticas de seguridad y límites de recursos, como la expiración de contraseñas, intentos fallidos de inicio de sesión o tiempo máximo de sesión.
```

---

# Pensamiento de Seguridad

Antes de crear un Profile pregúntate:

1. ¿Qué tipo de usuario lo utilizará?
2. ¿Qué políticas de contraseña requiere?
3. ¿Cuántos intentos fallidos permitiré?
4. ¿Debo limitar el tiempo de sesión?
5. ¿Existen restricciones de recursos?
6. ¿Cumplo con las políticas de seguridad de la empresa?
7. ¿Cómo revisaré y actualizaré estas políticas?

---

# Relación con los siguientes módulos

```text
ROLES AND PERMISSIONS
        ↓
PROFILES
        ↓
BACKUP AND RESTORE
        ↓
AUDITING
        ↓
DATABASE SECURITY
```

---

# Resumen

Los Profiles permiten aplicar políticas de seguridad y límites de recursos a los usuarios de una base de datos.

Conceptos principales:

- Políticas de contraseñas.
- Intentos fallidos de inicio de sesión.
- Tiempo de sesión.
- Tiempo de inactividad.
- Control de recursos.
- Administración centralizada.

Aunque su implementación varía entre los distintos DBMS, el concepto de aplicar políticas consistentes a los usuarios es una práctica fundamental de la administración moderna de bases de datos.
