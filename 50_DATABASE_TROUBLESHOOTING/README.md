# DATABASE TROUBLESHOOTING

## Definición

Database Troubleshooting es el proceso de identificar, analizar y resolver problemas que afectan el rendimiento, la disponibilidad o la estabilidad de una base de datos.

Su objetivo es restaurar el servicio lo más rápido posible y evitar que el problema vuelva a ocurrir.

---

# ¿Por qué existe?

Toda base de datos en producción enfrentará problemas.

Ejemplos:

```text
Consultas lentas

Bloqueos

Deadlocks

CPU elevada

Memoria insuficiente

Disco lleno

Fallas de replicación

Conexiones agotadas

Backups fallidos
```

---

Pregunta:

```text
¿Cómo encontramos

la causa

del problema?
```

---

La respuesta es:

```text
Database Troubleshooting.
```

---

# Concepto Fundamental

Resolver un problema no consiste en:

```text
Reiniciar

el servidor.
```

---

Consiste en:

```text
Detectar

↓

Analizar

↓

Corregir

↓

Validar

↓

Prevenir
```

---

# Flujo de Diagnóstico

```text
Incidente

↓

Identificación

↓

Análisis

↓

Corrección

↓

Validación

↓

Documentación
```

---

# Problemas Comunes

## Consultas Lentas

Síntomas:

```text
Reportes tardan minutos

Alta utilización de CPU

Usuarios reportan lentitud
```

---

Posibles causas:

```text
Falta de índices

Mal diseño

Estadísticas desactualizadas

Consultas ineficientes
```

---

Herramientas:

```text
EXPLAIN

Execution Plan

Query Analyzer
```

---

# Bloqueos (Locks)

Síntomas:

```text
Consultas esperando

Transacciones detenidas
```

---

Posibles causas:

```text
Transacciones largas

Actualizaciones masivas

Falta de COMMIT
```

---

# Deadlocks

Ocurren cuando:

```text
Transacción A

↓

Espera

↓

Transacción B

↓

Espera

↓

Transacción A
```

---

Resultado:

```text
Ninguna

puede continuar.
```

---

La mayoría de los DBMS detectan el deadlock y cancelan automáticamente una de las transacciones.

---

# CPU Elevada

Posibles causas:

```text
Consultas costosas

Falta de índices

Procesos concurrentes

Consultas repetitivas
```

---

# Uso Excesivo de Memoria

Puede deberse a:

```text
Buffer insuficiente

Consultas grandes

Configuración incorrecta
```

---

# Espacio en Disco

Problemas comunes:

```text
Logs muy grandes

Backups

Tablas temporales

Crecimiento inesperado
```

---

Una base de datos sin espacio puede:

```text
Detenerse.
```

---

# Problemas de Replicación

Ejemplos:

```text
Replication Lag

Replica detenida

Errores de sincronización
```

---

Impacto:

```text
Datos desactualizados

Failover comprometido
```

---

# Conexiones Agotadas

Síntomas:

```text
No se aceptan

nuevas conexiones.
```

---

Posibles causas:

```text
Connection Pool

mal configurado

Sesiones abiertas

Fugas de conexiones
```

---

# Backups Fallidos

Siempre verificar:

```text
Espacio disponible

Permisos

Logs

Integridad
```

---

# Metodología de Resolución

## Paso 1

Confirmar el problema.

---

## Paso 2

Revisar métricas.

```text
CPU

Memoria

Disco

Conexiones
```

---

## Paso 3

Analizar Logs.

---

## Paso 4

Identificar la causa raíz.

---

## Paso 5

Aplicar la solución.

---

## Paso 6

Validar que el problema desapareció.

---

## Paso 7

Documentar el incidente.

---

# Herramientas

## PostgreSQL

```text
EXPLAIN

pg_stat_activity

pg_stat_statements

Logs
```

---

## SQL Server

```text
Activity Monitor

Extended Events

Execution Plans

DMVs
```

---

## Oracle

```text
AWR

ASH

Oracle Enterprise Manager
```

---

## MySQL

```text
Performance Schema

Slow Query Log

EXPLAIN
```

---

# Caso Real

Empresa de E-commerce.

Problema:

```text
CPU

95%
```

---

Diagnóstico:

```text
Consulta

sin índice.
```

---

Solución:

```text
Crear índice.

Actualizar estadísticas.
```

---

Resultado:

```text
CPU

35%
```

---

# Buenas Prácticas

## No asumir la causa

Investigar antes de actuar.

---

## Revisar Logs

Siempre.

---

## Analizar el plan de ejecución

Antes de modificar consultas.

---

## Documentar incidentes

Permite aprender y prevenir.

---

## Automatizar alertas

Reducir el tiempo de respuesta.

---

## Monitorear continuamente

Detectar problemas antes que los usuarios.

---

# Error Común

Reiniciar:

```text
La base de datos

↓

Sin investigar.
```

---

Problema:

```text
El síntoma desaparece

↓

La causa permanece.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Toda lentitud

↓

Es culpa

de la base de datos.
```

---

Incorrecto.

También pueden influir:

```text
Aplicación

Red

Servidor

Almacenamiento

Infraestructura
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cómo abordarías

un problema

de rendimiento

en una base

de datos?
```

---

Respuesta:

```text
Primero confirmaría el problema revisando métricas y monitoreo. Después analizaría los logs y el plan de ejecución de las consultas involucradas para identificar la causa raíz. Aplicaría la solución correspondiente, validaría el resultado y documentaría el incidente para evitar recurrencias.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Cuáles son

las causas

más comunes

de consultas lentas?
```

---

Respuesta:

```text
Índices inexistentes o ineficientes, estadísticas desactualizadas, consultas mal diseñadas, grandes volúmenes de datos, bloqueos, planes de ejecución poco eficientes y limitaciones de recursos como CPU, memoria o almacenamiento.
```

---

# Pensamiento de un DBA

Ante cualquier incidente pregúntate:

1. ¿Cuál es el síntoma?
2. ¿Cuándo comenzó el problema?
3. ¿Qué cambió recientemente?
4. ¿Qué muestran las métricas?
5. ¿Qué indican los logs?
6. ¿Cuál es la causa raíz?
7. ¿Cómo evitaré que vuelva a ocurrir?

---

# Relación con el siguiente módulo

```text
DATABASE MAINTENANCE
        ↓
DATABASE TROUBLESHOOTING
        ↓
DBA BEST PRACTICES
```

---

# Resumen

Database Troubleshooting es el proceso de diagnosticar y resolver problemas en una base de datos mediante un enfoque estructurado basado en evidencia.

Conceptos principales:

- Consultas lentas.
- Bloqueos.
- Deadlocks.
- CPU y memoria.
- Espacio en disco.
- Replicación.
- Backups.
- Logs.
- Planes de ejecución.

Beneficios:

- Menor tiempo de resolución.
- Mayor disponibilidad.
- Mejor rendimiento.
- Diagnósticos más precisos.
- Prevención de incidentes futuros.

Un buen DBA no se limita a resolver problemas: identifica la causa raíz, implementa soluciones duraderas y documenta el conocimiento para mejorar continuamente la operación de la base de datos.
