# USER MANAGEMENT

## Definición

User Management es el proceso de crear, administrar y eliminar usuarios dentro de un Sistema de Gestión de Bases de Datos (DBMS).

Su objetivo es controlar quién puede acceder a la base de datos y qué acciones puede realizar.

---

# ¿Por qué existe?

En una empresa existen diferentes tipos de usuarios:

```text
Administradores

Desarrolladores

Analistas

Aplicaciones

Servicios ETL

Herramientas BI
```

---

Pregunta:

```text
¿Todos deberían tener
los mismos permisos?
```

---

Respuesta:

```text
No.
```

---

Cada usuario debe tener únicamente los permisos necesarios para realizar su trabajo.

Este principio se conoce como:

```text
Least Privilege
```

---

# Concepto Fundamental

Todo usuario representa una identidad que puede autenticarse contra el DBMS.

Un usuario puede:

- Conectarse.
- Ejecutar consultas.
- Crear objetos.
- Modificar datos.
- Administrar otros usuarios.

Todo depende de sus permisos.

---

# Arquitectura

```text
Application

      │

      ▼

 Database User

      │

      ▼

Database
```

---

# Ciclo de Vida de un Usuario

```text
Crear

↓

Configurar contraseña

↓

Asignar permisos

↓

Utilizar

↓

Modificar

↓

Deshabilitar

↓

Eliminar
```

---

# Crear un Usuario

La mayoría de los DBMS permiten crear usuarios.

Ejemplo (PostgreSQL):

```sql
CREATE USER analyst
WITH PASSWORD 'StrongPassword123';
```

---

Ejemplo (MySQL):

```sql
CREATE USER 'analyst'@'localhost'
IDENTIFIED BY 'StrongPassword123';
```

---

Ejemplo (SQL Server):

```sql
CREATE LOGIN analyst
WITH PASSWORD = 'StrongPassword123';
```

---

Ejemplo (Oracle):

```sql
CREATE USER analyst
IDENTIFIED BY StrongPassword123;
```

---

# Cambiar Contraseña

Ejemplo PostgreSQL

```sql
ALTER USER analyst
WITH PASSWORD 'NewPassword123';
```

---

Ejemplo MySQL

```sql
ALTER USER 'analyst'@'localhost'
IDENTIFIED BY 'NewPassword123';
```

---

# Renombrar Usuario

Algunos motores permiten renombrar usuarios.

Ejemplo PostgreSQL

```sql
ALTER USER analyst
RENAME TO data_analyst;
```

---

# Eliminar Usuario

Ejemplo PostgreSQL

```sql
DROP USER analyst;
```

---

Ejemplo MySQL

```sql
DROP USER 'analyst'@'localhost';
```

---

Antes de eliminar un usuario es importante verificar:

```text
Objetos creados

Permisos

Dependencias
```

---

# Usuarios de Aplicaciones

Es una buena práctica utilizar usuarios específicos para cada aplicación.

Ejemplo:

```text
crm_app

inventory_app

etl_service

powerbi_reader
```

---

Evitar compartir un mismo usuario entre múltiples aplicaciones.

---

# Usuarios Humanos

Ejemplos:

```text
juan.perez

ana.gomez

dba_admin

data_engineer
```

---

Cada persona debe tener su propia cuenta.

---

# Usuarios de Servicio

Utilizados por procesos automáticos.

Ejemplos:

```text
ETL

Airflow

Azure Data Factory

dbt

Kafka Connect
```

---

Generalmente:

- No inician sesión manualmente.
- Tienen permisos limitados.
- Utilizan autenticación segura.

---

# Buenas Prácticas

## Utilizar nombres descriptivos

Ejemplo:

```text
sales_app

etl_loader

finance_readonly
```

---

## Evitar compartir cuentas

Cada usuario debe ser individual.

---

## Eliminar cuentas inactivas

Reduce riesgos de seguridad.

---

## Utilizar contraseñas fuertes

Ejemplo:

- Mayúsculas
- Minúsculas
- Números
- Caracteres especiales

---

## Asignar únicamente los permisos necesarios

Aplicar el principio de:

```text
Least Privilege
```

---

# Error Común

Crear todas las aplicaciones utilizando:

```text
admin
```

---

Problemas:

- Riesgo de seguridad.
- Difícil auditoría.
- Exceso de privilegios.

---

# Error Conceptual Frecuente

Muchos creen:

```text
Usuario

=

Permisos.
```

---

Incorrecto.

Un usuario:

```text
Puede existir

↓

Sin permisos.
```

---

Los permisos normalmente se asignan mediante:

```text
Roles

o

GRANT.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Por qué no deberíamos
utilizar el usuario administrador
para una aplicación?
```

---

Respuesta:

```text
Porque viola el principio de menor privilegio (Least Privilege), incrementa el riesgo de seguridad y dificulta la auditoría de acciones realizadas por la aplicación.
```

---

# Pensamiento de Seguridad

Antes de crear un usuario pregúntate:

1. ¿Quién utilizará esta cuenta?
2. ¿Es una persona o una aplicación?
3. ¿Qué permisos necesita realmente?
4. ¿Podría reutilizar un rol existente?
5. ¿Cómo administraré la contraseña?
6. ¿Cómo auditaré sus acciones?
7. ¿Cuándo deberá deshabilitarse o eliminarse?

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
DATABASE SECURITY
```

---

# Resumen

User Management consiste en administrar las identidades que acceden a un DBMS.

Conceptos principales:

- Creación de usuarios.
- Modificación de cuentas.
- Eliminación de usuarios.
- Usuarios humanos.
- Usuarios de aplicaciones.
- Usuarios de servicio.
- Principio de menor privilegio.

Una correcta administración de usuarios es el primer paso para construir bases de datos seguras, auditables y fáciles de administrar.
