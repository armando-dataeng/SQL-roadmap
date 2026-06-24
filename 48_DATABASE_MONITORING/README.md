# DATABASE MONITORING

## Definición

Database Monitoring es el proceso continuo de observar, medir y analizar el estado de una base de datos para garantizar su rendimiento, disponibilidad, seguridad y estabilidad.

Su objetivo es detectar problemas antes de que afecten a los usuarios o a las aplicaciones.

---

# ¿Por qué existe?

Supongamos que una aplicación comienza a responder lentamente.

Pregunta:

```text
¿Qué está ocurriendo?

¿CPU alta?

¿Disco lleno?

¿Consultas lentas?

¿Bloqueos?
```

---

Sin monitoreo:

```text
No lo sabemos.
```

---

Con monitoreo:

```text
Detectamos

el problema

antes

de que afecte

al negocio.
```

---

# Concepto Fundamental

El monitoreo permite observar continuamente:

```text
Rendimiento

Disponibilidad

Recursos

Seguridad

Replicación

Backups
```

---

# Arquitectura

```text
Database

↓

Monitoring Agent

↓

Metrics

↓

Dashboard

↓

Alerts
```

---

El objetivo es transformar datos en información útil para la operación.

---

# ¿Qué debemos monitorear?

## Disponibilidad

Verificar que la base de datos esté operativa.

Ejemplos:

```text
Estado del servicio

Tiempo de actividad

Conectividad
```

---

## Rendimiento

Detectar degradaciones.

Ejemplos:

```text
Tiempo de respuesta

Consultas lentas

TPS

QPS
```

---

## CPU

Monitorear utilización.

Ejemplo:

```text
CPU > 90%
```

Puede indicar:

```text
Consultas ineficientes

Carga excesiva

Procesos anómalos
```

---

## Memoria

Controlar el consumo.

Ejemplos:

```text
Buffer Cache

Shared Memory

RAM utilizada
```

---

## Disco

Monitorear:

```text
Espacio libre

IOPS

Latencia

Crecimiento
```

---

Una base de datos sin espacio disponible:

```text
Puede detenerse.
```

---

## Conexiones

Ejemplos:

```text
Conexiones activas

Conexiones máximas

Sesiones bloqueadas
```

---

## Locks

Detectar:

```text
Locks

Deadlocks

Esperas
```

---

## Replicación

Si existe replicación:

```text
Estado

Lag

Sincronización
```

---

## Backups

Verificar:

```text
Último Backup

Resultado

Duración

Integridad
```

---

## Seguridad

Monitorear:

```text
Intentos fallidos

Usuarios bloqueados

Cambios de permisos

Eventos críticos
```

---

# Métricas Comunes

Ejemplos:

| Métrica | Descripción |
|----------|-------------|
| CPU Usage | Uso del procesador |
| Memory Usage | Consumo de memoria |
| Disk Usage | Espacio en disco |
| Active Sessions | Sesiones activas |
| Slow Queries | Consultas lentas |
| Replication Lag | Retraso de replicación |
| Uptime | Tiempo disponible |

---

# Alertas

El monitoreo debe generar alertas cuando se superen ciertos umbrales.

Ejemplos:

```text
CPU > 90%

Disco > 85%

Replica fuera de sincronización

Backup fallido

Conexiones máximas alcanzadas
```

---

# Dashboards

Los dashboards permiten visualizar:

```text
Disponibilidad

Consultas

CPU

Memoria

Disco

Replicación

Usuarios
```

---

# Herramientas

## PostgreSQL

```text
pg_stat_activity

pg_stat_statements
```

---

## Oracle

```text
Oracle Enterprise Manager
```

---

## SQL Server

```text
SQL Server Management Studio

SQL Server Profiler

Extended Events
```

---

## MySQL

```text
Performance Schema

MySQL Enterprise Monitor
```

---

## Herramientas Multiplataforma

```text
Prometheus

Grafana

Zabbix

Datadog

New Relic
```

---

# Caso Real

Empresa de E-commerce.

Se configura una alerta:

```text
CPU > 85%
```

---

El sistema detecta:

```text
Consulta lenta.
```

---

Resultado:

```text
Se optimiza

antes

de afectar

a los clientes.
```

---

# Beneficios

## Detección temprana

---

## Menor tiempo de inactividad

---

## Mejor rendimiento

---

## Mayor disponibilidad

---

## Mejor experiencia del usuario

---

# Buenas Prácticas

## Monitorear continuamente

No solo cuando ocurre un problema.

---

## Definir umbrales

Generar alertas automáticas.

---

## Centralizar métricas

Utilizar dashboards.

---

## Revisar tendencias

No enfocarse únicamente en incidentes.

---

## Automatizar notificaciones

Correo

Slack

Microsoft Teams

PagerDuty

---

## Monitorear Backups

No asumir que funcionan.

---

## Monitorear Replicación

Detectar retrasos rápidamente.

---

# Error Común

Pensar que:

```text
La base de datos

está funcionando

porque

nadie reporta problemas.
```

---

Problema:

```text
El incidente

ya ocurrió.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Monitorear

=

Ver CPU.
```

---

Incorrecto.

Debe incluir:

```text
Disponibilidad

Consultas

Bloqueos

Replicación

Backups

Seguridad

Disco

Memoria
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué métricas

deberían monitorearse

en una base de datos?
```

---

Respuesta:

```text
Disponibilidad, utilización de CPU, memoria, espacio en disco, consultas lentas, sesiones activas, bloqueos, replicación, Backups, eventos de seguridad y tiempos de respuesta.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Por qué

es importante

monitorear

Replication Lag?
```

---

Respuesta:

```text
Porque un retraso elevado entre el servidor principal y las réplicas puede provocar lecturas desactualizadas, afectar procesos de failover y aumentar el riesgo de pérdida de información durante una falla.
```

---

# Pensamiento de un DBA

Antes de implementar monitoreo pregúntate:

1. ¿Qué métricas son críticas para el negocio?
2. ¿Qué umbrales activarán alertas?
3. ¿Quién recibirá las notificaciones?
4. ¿Cómo almacenaré el histórico de métricas?
5. ¿Cómo detectaré tendencias?
6. ¿Qué herramientas utilizaré?
7. ¿Cómo responderé a una alerta crítica?

---

# Relación con los siguientes módulos

```text
DISASTER RECOVERY
        ↓
DATABASE MONITORING
        ↓
DATABASE MAINTENANCE
        ↓
DBA BEST PRACTICES
        ↓
DATABASE TROUBLESHOOTING
```

---

# Resumen

Database Monitoring consiste en observar continuamente el estado de una base de datos para garantizar su disponibilidad, rendimiento y seguridad.

Conceptos principales:

- Disponibilidad.
- CPU.
- Memoria.
- Disco.
- Consultas lentas.
- Bloqueos.
- Replicación.
- Backups.
- Alertas.
- Dashboards.

Beneficios:

- Detección temprana de problemas.
- Mayor disponibilidad.
- Mejor rendimiento.
- Respuesta rápida a incidentes.
- Operación proactiva.

El monitoreo continuo es una práctica esencial para cualquier entorno de producción y permite anticipar problemas antes de que impacten a los usuarios o al negocio.
