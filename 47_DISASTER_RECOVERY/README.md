# DISASTER RECOVERY (DR)

## Definición

Disaster Recovery (DR) es el conjunto de estrategias, procesos y tecnologías utilizadas para restaurar una base de datos y sus servicios después de un desastre que impide continuar operando en el entorno principal.

Su objetivo es minimizar la pérdida de datos y reducir el tiempo necesario para restablecer las operaciones del negocio.

---

# ¿Por qué existe?

Una base de datos puede dejar de estar disponible por causas como:

```text
Incendios

Inundaciones

Terremotos

Fallas eléctricas

Ataques de ransomware

Corrupción masiva

Errores humanos

Caída completa del centro de datos
```

---

Pregunta:

```text
¿Qué hacemos

si perdemos

todo el Data Center?
```

---

La respuesta es:

```text
Disaster Recovery.
```

---

# Concepto Fundamental

Un Disaster Recovery Plan define:

```text
Cómo recuperar

↓

La infraestructura

↓

Los datos

↓

Las aplicaciones

↓

Las operaciones.
```

---

No solo protege:

```text
La Base de Datos.
```

---

Protege:

```text
Todo el negocio.
```

---

# Arquitectura

```text
Primary Data Center

        │

        ▼

Replication

        │

        ▼

Disaster Recovery Site

        │

        ▼

Business Recovery
```

---

Si el sitio principal deja de funcionar:

```text
DR Site

↓

Asume

las operaciones.
```

---

# Componentes

Un plan DR normalmente incluye:

```text
Backups

Replicación

Sitio alterno

Procedimientos

Monitoreo

Pruebas
```

---

# Recovery Point Objective (RPO)

Define:

```text
¿Cuánta información

puede perder

el negocio?
```

---

Ejemplo:

```text
5 minutos.
```

---

Si ocurre un desastre:

```text
Máximo

5 minutos

de pérdida

de datos.
```

---

# Recovery Time Objective (RTO)

Define:

```text
¿Cuánto tiempo

puede permanecer

fuera de servicio

la organización?
```

---

Ejemplo:

```text
30 minutos.
```

---

# Tipos de Sitios

## Cold Site

Infraestructura mínima.

---

Ventajas:

```text
Menor costo.
```

---

Desventajas:

```text
Mayor tiempo

de recuperación.
```

---

# Warm Site

Infraestructura parcialmente preparada.

---

Ventajas:

```text
Balance

entre costo

y recuperación.
```

---

# Hot Site

Infraestructura completamente operativa.

---

Ventajas:

```text
Recuperación

muy rápida.
```

---

Desventajas:

```text
Mayor costo.
```

---

# Comparación

| Tipo | Tiempo de Recuperación | Costo |
|------|------------------------|-------|
| Cold Site | Alto | Bajo |
| Warm Site | Medio | Medio |
| Hot Site | Muy Bajo | Alto |

---

# Flujo de Recuperación

```text
Desastre

↓

Activación del DR Plan

↓

Recuperación

↓

Validación

↓

Reinicio del servicio
```

---

# Caso Real

Empresa Internacional.

Arquitectura:

```text
Primary Data Center

↓

Replication

↓

Cloud Disaster Recovery Site
```

---

Si ocurre un incendio:

```text
Cloud Site

↓

Continúa

la operación.
```

---

# DR vs Backup

## Backup

Permite recuperar datos.

---

## Disaster Recovery

Permite recuperar:

```text
Datos

Infraestructura

Aplicaciones

Operación.
```

---

# DR vs High Availability

High Availability:

```text
Protege

contra fallas

locales.
```

---

Disaster Recovery:

```text
Protege

contra

desastres

mayores.
```

---

# Tecnologías

Ejemplos:

```text
Azure Site Recovery

AWS Elastic Disaster Recovery

Oracle Data Guard

VMware Site Recovery Manager
```

---

# Beneficios

## Continuidad del negocio

---

## Reducción del Downtime

---

## Protección de datos

---

## Recuperación rápida

---

## Cumplimiento normativo

---

# Buenas Prácticas

## Definir RPO y RTO

Antes de diseñar la solución.

---

## Mantener Backups

En múltiples ubicaciones.

---

## Automatizar procesos

Reducir errores humanos.

---

## Probar el DR Plan

Regularmente.

---

## Documentar procedimientos

Todo el equipo debe conocerlos.

---

## Revisar el plan

Después de cambios importantes.

---

# Error Común

Pensar que:

```text
Replication

↓

Es suficiente.
```

---

Problema:

Si el Data Center desaparece:

```text
También

se pierde

la infraestructura.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
Disaster Recovery

=

Backup.
```

---

Incorrecto.

Un DR Plan incluye:

```text
Backups

Replicación

Infraestructura

Red

Aplicaciones

Procedimientos

Personal
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia

entre High Availability

y Disaster Recovery?
```

---

Respuesta:

```text
High Availability busca mantener el servicio disponible frente a fallas locales mediante redundancia y failover.

Disaster Recovery permite recuperar toda la operación después de un desastre mayor que afecta la infraestructura principal, utilizando sitios alternos, Backups, replicación y procedimientos documentados.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Qué significan

RPO

y

RTO?
```

---

Respuesta:

```text
RPO (Recovery Point Objective)

Es la cantidad máxima de datos que la organización está dispuesta a perder.

RTO (Recovery Time Objective)

Es el tiempo máximo permitido para restaurar el servicio después de un desastre.
```

---

# Pensamiento de un DBA

Antes de diseñar un Disaster Recovery Plan pregúntate:

1. ¿Qué eventos considero un desastre?
2. ¿Cuál es el RPO del negocio?
3. ¿Cuál es el RTO esperado?
4. ¿Dónde estará el sitio alterno?
5. ¿Cómo replicaré los datos?
6. ¿Cuándo fue la última prueba del DR Plan?
7. ¿Quién será responsable durante una recuperación?

---

# Relación con los siguientes módulos

```text
CLUSTERING
        ↓
DISASTER RECOVERY
        ↓
DATABASE MONITORING
        ↓
DATABASE MAINTENANCE
        ↓
DBA BEST PRACTICES
```

---

# Resumen

Disaster Recovery (DR) es el conjunto de estrategias utilizadas para recuperar una base de datos y toda la infraestructura tecnológica después de un desastre que impide continuar operando en el entorno principal.

Conceptos principales:

- Disaster Recovery Plan.
- RPO.
- RTO.
- Cold Site.
- Warm Site.
- Hot Site.
- Replicación.
- Backups.

Beneficios:

- Continuidad del negocio.
- Recuperación rápida.
- Protección frente a desastres.
- Reducción del impacto operativo.
- Cumplimiento de requisitos empresariales.

Un Disaster Recovery Plan bien diseñado garantiza que una organización pueda continuar operando incluso después de eventos catastróficos, convirtiéndose en un componente esencial de cualquier estrategia de continuidad del negocio.
