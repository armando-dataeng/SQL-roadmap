# DATABASE MAINTENANCE

## Definición

Database Maintenance es el conjunto de tareas preventivas y periódicas que permiten mantener una base de datos segura, eficiente, estable y disponible a lo largo del tiempo.

Su objetivo es prevenir problemas antes de que afecten el rendimiento o la disponibilidad del sistema.

---

# ¿Por qué existe?

Con el paso del tiempo una base de datos presenta:

```text
Mayor volumen de datos

Índices fragmentados

Estadísticas desactualizadas

Archivos de logs más grandes

Espacio desperdiciado

Consultas más lentas
```

---

Pregunta:

```text
¿Cómo mantenemos

la base de datos

en buen estado?
```

---

Respuesta:

```text
Database Maintenance.
```

---

# Concepto Fundamental

El mantenimiento consiste en ejecutar tareas periódicas para optimizar el funcionamiento del sistema.

Su objetivo es:

```text
Prevenir

↓

En lugar de

corregir.
```

---

# Arquitectura

```text
Database

↓

Maintenance Tasks

↓

Monitoring

↓

Optimization

↓

Healthy Database
```

---

# Tareas de Mantenimiento

## Actualizar estadísticas

Las estadísticas ayudan al optimizador a elegir el mejor plan de ejecución.

Si están desactualizadas:

```text
Consultas

más lentas.
```

---

Ejemplo SQL Server

```sql
UPDATE STATISTICS dbo.Customers;
```

---

Ejemplo PostgreSQL

```sql
ANALYZE;
```

---

# Reorganizar Índices

Con el tiempo los índices pueden fragmentarse.

Problema:

```text
Mayor cantidad

de lecturas.
```

---

Solución:

```text
Reorganizar índices.
```

---

# Reconstruir Índices

Cuando la fragmentación es alta.

Ejemplo SQL Server

```sql
ALTER INDEX ALL
ON Customers
REBUILD;
```

---

# Vacuum (PostgreSQL)

PostgreSQL reutiliza espacio mediante:

```text
VACUUM
```

---

Ejemplo

```sql
VACUUM;
```

---

También existe:

```sql
VACUUM ANALYZE;
```

---

# Limpiar Logs

Eliminar:

```text
Logs antiguos

Archivos temporales

Backups expirados
```

---

# Verificar Espacio

Monitorear:

```text
Disco

Tablespaces

Data Files

Transaction Logs
```

---

Una base de datos sin espacio puede detenerse.

---

# Validar Backups

Comprobar:

```text
Backups exitosos

Integridad

Restauraciones
```

---

Nunca asumir que un Backup funciona.

---

# Actualizar el DBMS

Las nuevas versiones incluyen:

```text
Correcciones

Optimización

Seguridad
```

---

Actualizar siguiendo un procedimiento controlado.

---

# Revisar Usuarios

Eliminar:

```text
Usuarios inactivos

Permisos innecesarios

Credenciales obsoletas
```

---

# Monitorear Crecimiento

Observar:

```text
Tamaño de tablas

Índices

Logs

Bases de datos
```

---

Permite planificar capacidad.

---

# Automatización

Las tareas de mantenimiento normalmente se ejecutan mediante:

```text
Cron

SQL Server Agent

Oracle Scheduler

Windows Task Scheduler

Airflow
```

---

# Calendario de Mantenimiento

Ejemplo:

```text
Diario

↓

Backups

Verificación

Monitoreo
```

---

```text
Semanal

↓

Reorganización

de índices
```

---

```text
Mensual

↓

Reconstrucción

de índices

Actualización

del sistema
```

---

# Beneficios

## Mejor rendimiento

---

## Mayor estabilidad

---

## Menor tiempo de inactividad

---

## Mayor seguridad

---

## Mejor utilización del almacenamiento

---

# Caso Real

Empresa Retail.

Cada noche:

```text
Backups

↓

VACUUM

↓

Actualización

de estadísticas

↓

Verificación

de integridad
```

---

Resultado:

```text
Consultas rápidas

↓

Sistema estable.
```

---

# Buenas Prácticas

## Automatizar tareas

---

## Actualizar estadísticas

Regularmente.

---

## Revisar fragmentación

De índices.

---

## Validar Backups

Siempre.

---

## Supervisar crecimiento

De la base de datos.

---

## Documentar procedimientos

---

## Programar ventanas

De mantenimiento.

---

# Error Común

Realizar mantenimiento:

```text
Solo

cuando

aparecen problemas.
```

---

Resultado:

```text
Mayor Downtime

↓

Mayor impacto

para el negocio.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Mantenimiento

=

Actualizar

la versión

del DBMS.
```

---

Incorrecto.

El mantenimiento incluye:

```text
Backups

Índices

Estadísticas

Logs

Espacio

Seguridad

Monitoreo
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué tareas

de mantenimiento

realizarías

periódicamente

en una base

de datos?
```

---

Respuesta:

```text
Actualizar estadísticas, reorganizar o reconstruir índices, validar Backups, monitorear el crecimiento de la base de datos, revisar el espacio disponible, limpiar archivos innecesarios, actualizar el DBMS cuando corresponda y verificar la seguridad de usuarios y permisos.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Por qué

es importante

actualizar

las estadísticas?
```

---

Respuesta:

```text
Porque el optimizador de consultas utiliza las estadísticas para seleccionar el plan de ejecución más eficiente.

Si las estadísticas están desactualizadas, el optimizador puede elegir planes poco eficientes y degradar el rendimiento de las consultas.
```

---

# Pensamiento de un DBA

Antes de definir un plan de mantenimiento pregúntate:

1. ¿Qué tareas deben ejecutarse diariamente?
2. ¿Cuáles pueden realizarse semanal o mensualmente?
3. ¿Cómo automatizaré el mantenimiento?
4. ¿Cómo validaré que las tareas se ejecutaron correctamente?
5. ¿Qué impacto tendrá sobre los usuarios?
6. ¿Existe una ventana de mantenimiento?
7. ¿Cómo documentaré los procedimientos?

---

# Relación con los siguientes módulos

```text
DATABASE MONITORING
        ↓
DATABASE MAINTENANCE
        ↓
DATABASE TROUBLESHOOTING
        ↓
DBA BEST PRACTICES
```

---

# Resumen

Database Maintenance reúne las tareas preventivas necesarias para mantener una base de datos en condiciones óptimas de funcionamiento.

Conceptos principales:

- Actualización de estadísticas.
- Reorganización y reconstrucción de índices.
- VACUUM.
- Validación de Backups.
- Gestión del espacio.
- Actualización del DBMS.
- Automatización de tareas.

Beneficios:

- Mejor rendimiento.
- Mayor estabilidad.
- Reducción de incidentes.
- Optimización del almacenamiento.
- Mayor disponibilidad.

Un plan de mantenimiento bien diseñado permite prolongar la vida útil de una base de datos, reducir problemas de rendimiento y garantizar una operación confiable en entornos de producción.
