# BACKUP AND RESTORE

## Definición

Backup and Restore es el conjunto de procesos utilizados para proteger una base de datos mediante la creación de copias de seguridad (Backups) y su posterior recuperación (Restore) en caso de pérdida de datos, corrupción o desastres.

Es uno de los pilares de la administración de bases de datos.

---

# ¿Por qué existen?

Las bases de datos pueden perder información debido a:

```text
Errores humanos

Fallas de hardware

Ataques de ransomware

Errores de software

Desastres naturales

Corrupción de datos
```

---

Pregunta:

```text
¿Cómo recuperamos
la información?
```

---

Respuesta:

```text
Backups.
```

---

# Concepto Fundamental

Todo plan de respaldo tiene dos objetivos:

```text
Respaldar datos

↓

Recuperar datos
```

---

Un Backup sin la capacidad de restaurarlo:

```text
No tiene valor.
```

---

# Arquitectura

```text
Database

↓

Backup

↓

Storage

↓

Restore

↓

Database Recovery
```

---

# ¿Qué es un Backup?

Un Backup es una copia de la información almacenada en una base de datos.

Su objetivo es permitir la recuperación de los datos cuando ocurre un incidente.

---

# ¿Qué es un Restore?

Un Restore consiste en recuperar una base de datos utilizando uno o varios Backups previamente generados.

---

# Tipos de Backup

## Full Backup

Realiza una copia completa de la base de datos.

---

Ventajas:

```text
Recuperación sencilla.
```

---

Desventajas:

```text
Mayor tiempo.

Mayor almacenamiento.
```

---

# Incremental Backup

Respalda únicamente los cambios realizados desde el último Backup.

---

Ventajas:

```text
Más rápido.

Menor espacio.
```

---

Desventajas:

```text
Recuperación más compleja.
```

---

# Differential Backup

Guarda todos los cambios realizados desde el último Full Backup.

---

Ventajas:

```text
Recuperación más rápida
que un incremental.
```

---

Desventajas:

```text
Ocupa más espacio
que un incremental.
```

---

# Comparación

| Tipo | Tamaño | Tiempo Backup | Tiempo Restore |
|------|---------|---------------|----------------|
| Full | Alto | Alto | Bajo |
| Incremental | Bajo | Bajo | Alto |
| Differential | Medio | Medio | Medio |

---

# Estrategia Típica

```text
Domingo

↓

Full Backup

↓

Lunes

↓

Incremental

↓

Martes

↓

Incremental

↓

Miércoles

↓

Incremental
```

---

# Ejemplo PostgreSQL

Backup

```bash
pg_dump company > company.sql
```

---

Restore

```bash
psql company < company.sql
```

---

# Ejemplo MySQL

Backup

```bash
mysqldump -u root -p company > company.sql
```

---

Restore

```bash
mysql -u root -p company < company.sql
```

---

# Ejemplo SQL Server

Backup

```sql
BACKUP DATABASE Sales
TO DISK = 'C:\Backup\Sales.bak';
```

---

Restore

```sql
RESTORE DATABASE Sales
FROM DISK = 'C:\Backup\Sales.bak';
```

---

# Ejemplo Oracle

Oracle utiliza:

```text
RMAN

(Recovery Manager)
```

---

Backup

```text
RMAN BACKUP DATABASE
```

---

Restore

```text
RMAN RESTORE DATABASE
```

---

# Recovery Point Objective (RPO)

Define:

```text
¿Cuánta información
puedo perder?
```

---

Ejemplo:

```text
15 minutos.
```

---

# Recovery Time Objective (RTO)

Define:

```text
¿Cuánto tiempo
puedo tardar
en recuperar
el servicio?
```

---

Ejemplo:

```text
30 minutos.
```

---

# Estrategia 3-2-1

Una buena práctica consiste en mantener:

```text
3 copias

↓

2 medios diferentes

↓

1 copia fuera del sitio
```

---

Ejemplo:

```text
Servidor

↓

NAS

↓

Cloud Storage
```

---

# Automatización

Los Backups deben ejecutarse automáticamente mediante:

```text
Cron

SQL Server Agent

Oracle Scheduler

Windows Task Scheduler

Airflow
```

---

Nunca depender de procesos manuales.

---

# Validación

Después de crear un Backup es recomendable:

```text
Verificar integridad.

↓

Realizar una restauración
de prueba.

↓

Validar la información.
```

---

# Caso Real

Empresa Retail.

Objetivo:

```text
RPO

15 minutos.
```

---

RTO:

```text
1 hora.
```

---

Estrategia:

```text
Full Backup

↓

Diario

↓

Incremental

↓

Cada 15 minutos
```

---

# Buenas Prácticas

## Automatizar Backups

Nunca ejecutarlos manualmente.

---

## Probar Restauraciones

Un Backup no probado no garantiza recuperación.

---

## Mantener múltiples copias

Aplicar la estrategia 3-2-1.

---

## Cifrar los Backups

Especialmente fuera del sitio.

---

## Monitorear el proceso

Detectar fallos inmediatamente.

---

## Documentar el procedimiento

Facilita la recuperación en incidentes.

---

# Error Común

Crear Backups:

```text
Nunca probarlos.
```

---

Resultado:

```text
Falla el Restore

↓

Pérdida de datos.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Backup

=

Alta Disponibilidad.
```

---

Incorrecto.

Un Backup protege contra:

```text
Pérdida de datos.
```

---

La Alta Disponibilidad busca:

```text
Mantener el servicio disponible.
```

---

Son estrategias complementarias.

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia
entre un Full Backup
y un Incremental Backup?
```

---

Respuesta:

```text
Un Full Backup copia toda la base de datos.

Un Incremental Backup solo copia los cambios realizados desde el último Backup, reduciendo tiempo y almacenamiento, aunque hace más compleja la recuperación.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Qué significan
RPO y RTO?
```

---

Respuesta:

```text
RPO (Recovery Point Objective)

Define la cantidad máxima de datos que la organización está dispuesta a perder.

RTO (Recovery Time Objective)

Define el tiempo máximo permitido para restaurar el servicio después de un incidente.
```

---

# Pensamiento de un DBA

Antes de diseñar una estrategia de Backups pregúntate:

1. ¿Cuál es el RPO del negocio?
2. ¿Cuál es el RTO esperado?
3. ¿Con qué frecuencia debo respaldar?
4. ¿Dónde almacenaré los Backups?
5. ¿Cómo protegeré los Backups?
6. ¿Cómo automatizaré el proceso?
7. ¿Cuándo fue la última restauración exitosa?

---

# Relación con los siguientes módulos

```text
PROFILES
        ↓
BACKUP AND RESTORE
        ↓
AUDITING
        ↓
DATABASE SECURITY
        ↓
HIGH AVAILABILITY
```

---

# Resumen

Backup and Restore es el conjunto de procesos que protege una base de datos frente a pérdidas de información y permite recuperarla cuando ocurre un incidente.

Conceptos principales:

- Full Backup
- Incremental Backup
- Differential Backup
- Restore
- RPO
- RTO
- Estrategia 3-2-1

Buenas prácticas:

- Automatizar los Backups.
- Cifrar las copias de seguridad.
- Mantener múltiples ubicaciones.
- Probar periódicamente las restauraciones.
- Documentar el procedimiento de recuperación.

Una estrategia sólida de Backup and Restore es esencial para garantizar la continuidad del negocio y minimizar el impacto de fallos o desastres.
