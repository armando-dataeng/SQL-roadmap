# AUDITING

## Definición

Database Auditing es el proceso de registrar y monitorear las actividades realizadas dentro de una base de datos.

Su objetivo es mantener un historial de las acciones ejecutadas por usuarios y aplicaciones para mejorar la seguridad, facilitar investigaciones y cumplir con requisitos regulatorios.

---

# ¿Por qué existe?

Supongamos que un día desaparecen miles de registros.

Pregunta:

```text
¿Quién los eliminó?

¿Cuándo ocurrió?

¿Qué usuario ejecutó la acción?

¿Desde qué aplicación?
```

---

Sin auditoría:

```text
No lo sabemos.
```

---

Con auditoría:

```text
Toda la actividad
queda registrada.
```

---

# Concepto Fundamental

La auditoría registra eventos como:

```text
Inicio de sesión

Cierre de sesión

Consultas

Inserciones

Actualizaciones

Eliminaciones

Cambios de permisos

Creación de objetos
```

---

# Arquitectura

```text
Users

↓

Database

↓

Audit Log

↓

Auditor
```

---

# ¿Qué puede auditarse?

## Autenticación

Ejemplos:

```text
Login

Logout

Intentos fallidos
```

---

## Acceso a Datos

Ejemplos:

```text
SELECT

INSERT

UPDATE

DELETE
```

---

## Cambios de Estructura

Ejemplos:

```text
CREATE TABLE

ALTER TABLE

DROP TABLE
```

---

## Administración

Ejemplos:

```text
GRANT

REVOKE

CREATE USER

DROP USER
```

---

# Información Registrada

Normalmente un registro de auditoría contiene:

```text
Usuario

Fecha y hora

Dirección IP

Aplicación

Base de datos

Acción ejecutada

Objeto afectado

Resultado
```

---

Ejemplo

| Usuario | Acción | Tabla | Fecha |
|----------|---------|--------|---------|
| juan | DELETE | Orders | 2025-01-15 14:22 |

---

# Tipos de Auditoría

## Login Auditing

Registra conexiones.

---

Ejemplo:

```text
Login exitoso

Login fallido

Logout
```

---

## DML Auditing

Registra cambios en datos.

---

Ejemplos:

```text
INSERT

UPDATE

DELETE
```

---

## DDL Auditing

Registra cambios en la estructura.

---

Ejemplos:

```text
CREATE

ALTER

DROP
```

---

## Privilege Auditing

Registra cambios de permisos.

---

Ejemplos:

```text
GRANT

REVOKE
```

---

# Ejemplo Oracle

Auditar sesiones:

```sql
AUDIT SESSION;
```

---

Auditar creación de tablas:

```sql
AUDIT CREATE TABLE;
```

---

# Ejemplo SQL Server

SQL Server ofrece:

```text
SQL Server Audit
```

Permite registrar:

- Logins
- Cambios
- Consultas
- Permisos

---

# PostgreSQL

PostgreSQL utiliza extensiones como:

```text
pgAudit
```

Para registrar:

```text
SELECT

INSERT

UPDATE

DELETE

DDL
```

---

# MySQL

MySQL Enterprise incluye:

```text
Audit Log Plugin
```

También existen soluciones de terceros para versiones Community.

---

# Caso Real

Empresa Financiera.

Se requiere saber:

```text
¿Quién modificó

el saldo

de una cuenta?
```

---

El Audit Log registra:

```text
Usuario

Hora

IP

Consulta

Resultado
```

---

La investigación puede realizarse rápidamente.

---

# Beneficios

## Seguridad

Detecta actividades sospechosas.

---

## Cumplimiento

Facilita regulaciones como:

```text
GDPR

HIPAA

PCI DSS

SOX
```

---

## Trazabilidad

Permite reconstruir eventos.

---

## Investigación

Facilita análisis forenses.

---

## Gobierno

Mayor control sobre la información.

---

# Buenas Prácticas

## Auditar operaciones críticas

No es necesario registrar absolutamente todo.

---

## Proteger los Audit Logs

Evitar modificaciones.

---

## Definir períodos de retención

Conservar registros según la política de la organización.

---

## Monitorear eventos sospechosos

Automatizar alertas.

---

## Revisar periódicamente

Los registros de auditoría.

---

# Error Común

Registrar:

```text
Todas las consultas.
```

---

Resultado:

```text
Logs enormes.

Mayor consumo.

Difícil análisis.
```

---

La auditoría debe enfocarse en:

```text
Eventos críticos.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Auditoría

=

Backup.
```

---

Incorrecto.

```text
Backup

↓

Recupera datos.
```

---

```text
Auditoría

↓

Registra actividades.
```

---

Son procesos diferentes.

---

# Caso de Entrevista

Pregunta:

```text
¿Qué información
debería contener
un Audit Log?
```

---

Respuesta:

```text
Un Audit Log debe registrar, como mínimo:

- Usuario
- Fecha y hora
- Acción ejecutada
- Objeto afectado
- Resultado
- Dirección IP o aplicación de origen (cuando sea posible)
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Por qué no es recomendable
auditar absolutamente
todas las operaciones?
```

---

Respuesta:

```text
Porque genera grandes volúmenes de datos, incrementa el consumo de recursos y dificulta el análisis.

Es preferible auditar operaciones críticas y aquellas requeridas por las políticas de seguridad o normativas.
```

---

# Pensamiento de un DBA

Antes de habilitar la auditoría pregúntate:

1. ¿Qué eventos necesito registrar?
2. ¿Qué exige la normativa aplicable?
3. ¿Dónde almacenaré los Audit Logs?
4. ¿Cuánto tiempo debo conservarlos?
5. ¿Cómo protegeré los registros?
6. ¿Cómo detectaré actividades sospechosas?
7. ¿Qué impacto tendrá sobre el rendimiento?

---

# Relación con los siguientes módulos

```text
BACKUP AND RESTORE
        ↓
AUDITING
        ↓
DATABASE SECURITY
        ↓
HIGH AVAILABILITY
        ↓
REPLICATION
```

---

# Resumen

Database Auditing permite registrar y monitorear las actividades realizadas dentro de una base de datos para mejorar la seguridad, la trazabilidad y el cumplimiento normativo.

Conceptos principales:

- Login Auditing
- DML Auditing
- DDL Auditing
- Privilege Auditing
- Audit Logs

Beneficios:

- Seguridad.
- Trazabilidad.
- Investigación de incidentes.
- Cumplimiento regulatorio.
- Gobierno de datos.

Una estrategia de auditoría bien diseñada permite saber quién hizo qué, cuándo lo hizo y sobre qué objeto, convirtiéndose en un componente esencial de cualquier plataforma de bases de datos empresarial.
