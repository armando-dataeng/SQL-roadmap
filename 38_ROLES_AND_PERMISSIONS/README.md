# ROLES AND PERMISSIONS

## Definición

Los Roles y Permisos permiten controlar las acciones que un usuario puede realizar dentro de una base de datos.

En lugar de asignar permisos individualmente a cada usuario, los permisos normalmente se agrupan en roles que luego son asignados a los usuarios.

Este modelo facilita la administración y mejora la seguridad.

---

# ¿Por qué existen?

Supongamos una empresa con:

```text
20 Desarrolladores

15 Analistas

5 DBAs

10 Aplicaciones
```

---

Pregunta:

```text
¿Debemos asignar permisos
uno por uno
a cada usuario?
```

---

Respuesta:

```text
No.
```

---

La solución es:

```text
Roles.
```

---

# Concepto Fundamental

Un:

```text
Usuario
```

representa una identidad.

---

Un:

```text
Rol
```

representa un conjunto de permisos.

---

Arquitectura:

```text
Usuario

↓

Rol

↓

Permisos
```

---

# ¿Qué es un Permiso?

Un permiso autoriza una acción sobre un objeto.

Ejemplos:

```text
SELECT

INSERT

UPDATE

DELETE

EXECUTE

CREATE

ALTER

DROP
```

---

# ¿Qué es un Rol?

Un rol es una colección de permisos.

Ejemplo:

```text
Role:

Analyst
```

Permisos:

```text
SELECT

EXECUTE
```

---

Otro ejemplo:

```text
Role:

Developer
```

Permisos:

```text
SELECT

INSERT

UPDATE

DELETE
```

---

# Arquitectura

```text
Developer

↓

Developer Role

↓

SELECT

INSERT

UPDATE

DELETE
```

---

# Asignar Permisos

Ejemplo PostgreSQL

```sql
GRANT SELECT
ON customers
TO analyst;
```

---

Ejemplo MySQL

```sql
GRANT SELECT
ON sales.*
TO 'analyst'@'localhost';
```

---

# Revocar Permisos

Ejemplo:

```sql
REVOKE INSERT
ON customers
FROM analyst;
```

---

El usuario conserva los demás permisos.

---

# Crear un Rol

Ejemplo PostgreSQL

```sql
CREATE ROLE analyst;
```

---

Ejemplo Oracle

```sql
CREATE ROLE analyst;
```

---

# Asignar Permisos al Rol

```sql
GRANT SELECT
ON customers
TO analyst;
```

---

# Asignar el Rol al Usuario

Ejemplo PostgreSQL

```sql
GRANT analyst
TO juan;
```

---

Resultado:

```text
Juan

↓

Role Analyst

↓

SELECT
```

---

# Principio de Menor Privilegio

Todo usuario debe tener:

```text
Solo los permisos necesarios.
```

---

No más.

---

Ejemplo

Analista:

```text
SELECT
```

---

No necesita:

```text
DROP TABLE
```

---

# Tipos de Roles

## DBA

Permisos completos.

---

## Developer

Puede modificar estructuras.

---

## Analyst

Lectura únicamente.

---

## ETL

Carga de datos.

---

## BI

Consultas analíticas.

---

## Application

Acceso limitado.

---

# Permisos Comunes

## SELECT

Leer datos.

---

## INSERT

Insertar registros.

---

## UPDATE

Modificar registros.

---

## DELETE

Eliminar registros.

---

## EXECUTE

Ejecutar procedimientos.

---

## CREATE

Crear objetos.

---

## ALTER

Modificar objetos.

---

## DROP

Eliminar objetos.

---

# Caso Real

Empresa Retail.

Usuarios:

```text
Power BI

↓

Solo lectura.
```

---

Developer

↓

```text
SELECT

INSERT

UPDATE
```

---

DBA

↓

```text
Todos los permisos.
```

---

# Roles por Aplicación

Ejemplo:

```text
crm_app

inventory_app

etl_loader

powerbi_reader
```

---

Cada uno recibe únicamente los permisos necesarios.

---

# Roles Jerárquicos

Algunos DBMS permiten:

```text
Roles

↓

Dentro

↓

De otros roles.
```

---

Ejemplo:

```text
ReadOnly

↓

Analyst

↓

FinanceAnalyst
```

---

Facilita la administración.

---

# Buenas Prácticas

## Utilizar Roles

No asignar permisos directamente.

---

## Aplicar Least Privilege

Siempre.

---

## Revisar permisos periódicamente

Eliminar accesos innecesarios.

---

## Utilizar nombres descriptivos

Ejemplo:

```text
finance_reader

sales_writer

etl_loader
```

---

## Documentar permisos

Especialmente en ambientes empresariales.

---

# Error Común

Asignar:

```text
DBA

↓

A todos.
```

---

Resultado:

```text
Riesgo de seguridad.

Errores accidentales.

Difícil auditoría.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Usuario

↓

Permisos.
```

---

La mejor práctica es:

```text
Usuario

↓

Rol

↓

Permisos.
```

---

Esto simplifica la administración.

---

# Caso de Entrevista

Pregunta:

```text
¿Por qué utilizar roles
en lugar de asignar permisos
directamente a los usuarios?
```

---

Respuesta:

```text
Porque los roles centralizan la administración de permisos, facilitan la reutilización, reducen errores y permiten aplicar el principio de menor privilegio de forma consistente.
```

---

# Pensamiento de Seguridad

Antes de asignar permisos pregúntate:

1. ¿Qué necesita hacer realmente este usuario?
2. ¿Existe un rol que ya cubra esa necesidad?
3. ¿Estoy otorgando permisos innecesarios?
4. ¿Cómo auditaré este acceso?
5. ¿Qué impacto tendría un uso indebido?
6. ¿Quién aprobará estos permisos?
7. ¿Cuándo deberán revisarse o revocarse?

---

# Relación con los siguientes módulos

```text
USER MANAGEMENT
        ↓
ROLES AND PERMISSIONS
        ↓
PROFILES
        ↓
BACKUP AND RESTORE
        ↓
AUDITING
```

---

# Resumen

Los Roles y Permisos permiten controlar el acceso a los recursos de una base de datos de forma segura y organizada.

Conceptos principales:

- Usuarios
- Roles
- Permisos
- GRANT
- REVOKE
- Least Privilege

Beneficios:

- Administración centralizada.
- Mayor seguridad.
- Menor riesgo de errores.
- Facilidad de mantenimiento.
- Escalabilidad.

El uso de roles es una práctica recomendada en todos los sistemas gestores de bases de datos modernos y constituye uno de los fundamentos de la administración y seguridad de bases de datos.
