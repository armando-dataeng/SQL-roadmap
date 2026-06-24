# REPLICATION

## Definición

Database Replication es el proceso de copiar y sincronizar datos desde una base de datos origen hacia una o más bases de datos destino.

Su objetivo es mejorar la disponibilidad, la escalabilidad, la recuperación ante fallos y el rendimiento de las consultas.

La replicación es uno de los componentes fundamentales de las arquitecturas modernas de bases de datos.

---

# ¿Por qué existe?

Supongamos una empresa con millones de usuarios.

Pregunta:

```text
¿Puede un solo servidor
manejar todas las consultas?
```

---

En muchos casos:

```text
No.
```

---

La solución es:

```text
Replication.
```

---

# Concepto Fundamental

Existe una base de datos principal que replica su información hacia uno o varios servidores secundarios.

Arquitectura:

```text
Primary Database

↓

Replica Database

↓

Replica Database
```

---

Todos contienen la misma información (o una copia sincronizada).

---

# Arquitectura

```text
Applications

        │

        ▼

Primary Database

        │

        ▼

---------------------

Replica 1

Replica 2

Replica 3
```

---

Normalmente:

```text
Primary

↓

Lecturas + Escrituras
```

---

```text
Replicas

↓

Lecturas
```

---

# Componentes

## Primary

Servidor principal.

Recibe:

```text
INSERT

UPDATE

DELETE
```

---

## Replica

Servidor secundario.

Generalmente recibe únicamente:

```text
SELECT
```

---

# Flujo

```text
Application

↓

Primary

↓

Replication

↓

Replica
```

---

Cada cambio realizado en el Primary es enviado a las réplicas.

---

# Tipos de Replicación

## Replicación Sincrónica

El Primary espera a que la réplica confirme la escritura.

---

Ventajas

```text
Mayor consistencia.
```

---

Desventajas

```text
Mayor latencia.
```

---

## Replicación Asincrónica

El Primary responde inmediatamente.

Las réplicas se actualizan posteriormente.

---

Ventajas

```text
Mayor rendimiento.
```

---

Desventajas

```text
Puede existir retraso.
```

---

# Comparación

| Característica | Sincrónica | Asincrónica |
|---------------|------------|-------------|
| Consistencia | Muy alta | Alta |
| Latencia | Mayor | Menor |
| Riesgo de pérdida | Muy bajo | Puede existir |
| Rendimiento | Menor | Mayor |

---

# Replicación Física

Replica bloques físicos del almacenamiento.

---

Ejemplo:

PostgreSQL Streaming Replication.

---

Ventajas:

```text
Rápida.

Simple.
```

---

# Replicación Lógica

Replica objetos y cambios lógicos.

Ejemplo:

```text
Tablas

Filas

Transacciones
```

---

Ventajas:

```text
Mayor flexibilidad.
```

---

# Caso Real

Empresa Global.

Usuarios:

```text
Europa

América

Asia
```

---

Arquitectura:

```text
Primary

↓

Replica Europa

↓

Replica América

↓

Replica Asia
```

---

Resultado:

```text
Consultas más rápidas
para cada región.
```

---

# Beneficios

## Mayor disponibilidad

---

## Escalabilidad

Distribuye las consultas.

---

## Balanceo de carga

Reduce presión sobre el servidor principal.

---

## Recuperación rápida

Facilita estrategias de Failover.

---

## Reportes

Las consultas analíticas pueden ejecutarse sobre las réplicas.

---

# Casos de Uso

## High Availability

---

## Disaster Recovery

---

## Reportes

---

## Business Intelligence

---

## Lecturas distribuidas

---

## Migraciones

---

# Tecnologías

## PostgreSQL

```text
Streaming Replication

Logical Replication
```

---

## MySQL

```text
Replication

Group Replication
```

---

## SQL Server

```text
Transactional Replication

Merge Replication

Snapshot Replication
```

---

## Oracle

```text
Data Guard

GoldenGate
```

---

# Replication vs Backup

## Replication

Mantiene una copia sincronizada.

---

## Backup

Permite recuperar información histórica.

---

La replicación:

```text
No reemplaza

los Backups.
```

---

# Replication vs High Availability

Replication:

```text
Copia datos.
```

---

High Availability:

```text
Mantiene el servicio disponible.
```

---

La replicación suele formar parte de una solución HA.

---

# Buenas Prácticas

## Monitorear el retraso de las réplicas

Evitar grandes diferencias con el Primary.

---

## Probar el Failover

Verificar que las réplicas puedan asumir el rol principal.

---

## Mantener la red estable

La replicación depende de una comunicación confiable.

---

## Utilizar Backups

La replicación no protege frente a errores lógicos o eliminaciones accidentales.

---

## Supervisar el estado de sincronización

Detectar problemas rápidamente.

---

# Error Común

Pensar que:

```text
Replication

=

Backup.
```

---

Problema:

Si se elimina información en el Primary:

```text
También

se elimina

en las réplicas.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Replication

↓

Garantiza

High Availability.
```

---

Incorrecto.

La replicación es:

```text
Un componente

de una arquitectura

de High Availability.
```

---

También se requieren:

```text
Failover

Monitoreo

Automatización
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia
entre Replication
y Backup?
```

---

Respuesta:

```text
La replicación mantiene una copia sincronizada de la base de datos para mejorar disponibilidad y rendimiento.

Los Backups crean copias independientes que permiten recuperar información después de pérdidas de datos o corrupción.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Cuál es la diferencia
entre replicación
sincrónica
y asincrónica?
```

---

Respuesta:

```text
En la replicación sincrónica el servidor principal espera la confirmación de la réplica antes de completar la operación, garantizando mayor consistencia.

En la replicación asincrónica el servidor principal responde inmediatamente y las réplicas se actualizan posteriormente, ofreciendo mejor rendimiento pero con un posible retraso en la sincronización.
```

---

# Pensamiento de un DBA

Antes de implementar replicación pregúntate:

1. ¿Necesito mejorar disponibilidad o rendimiento?
2. ¿Las réplicas atenderán consultas de lectura?
3. ¿Prefiero consistencia o menor latencia?
4. ¿Cómo monitorearé el retraso de las réplicas?
5. ¿Qué ocurrirá si falla el servidor principal?
6. ¿Cómo realizaré el failover?
7. ¿Cómo combinaré replicación y Backups?

---

# Relación con los siguientes módulos

```text
HIGH AVAILABILITY
        ↓
REPLICATION
        ↓
CLUSTERING
        ↓
DISASTER RECOVERY
        ↓
DATABASE MONITORING
```

---

# Resumen

Database Replication permite copiar y sincronizar datos entre múltiples servidores para mejorar la disponibilidad, el rendimiento y la escalabilidad.

Conceptos principales:

- Primary Database.
- Replica Database.
- Replicación sincrónica.
- Replicación asincrónica.
- Replicación física.
- Replicación lógica.

Beneficios:

- Mayor disponibilidad.
- Escalabilidad.
- Balanceo de carga.
- Soporte para High Availability.
- Mejor rendimiento en consultas.

La replicación es un componente esencial de las arquitecturas modernas de bases de datos, pero no reemplaza a los Backups ni, por sí sola, garantiza una solución completa de High Availability.
