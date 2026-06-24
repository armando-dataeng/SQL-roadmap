# HIGH AVAILABILITY (HA)

## Definición

High Availability (HA) es el conjunto de arquitecturas, tecnologías y estrategias utilizadas para mantener una base de datos disponible con el menor tiempo de inactividad posible, incluso cuando ocurre una falla de hardware, software o red.

Su objetivo es garantizar la continuidad del servicio.

---

# ¿Por qué existe?

Las bases de datos soportan aplicaciones críticas como:

```text
Bancos

E-commerce

Hospitales

Aerolíneas

Sistemas ERP
```

---

Pregunta:

```text
¿Qué ocurre

si el servidor

de la base de datos

deja de funcionar?
```

---

Sin HA:

```text
La aplicación
queda fuera de servicio.
```

---

Con HA:

```text
Otro servidor

continúa

prestando el servicio.
```

---

# Concepto Fundamental

High Availability busca:

```text
Minimizar

↓

El tiempo

↓

De inactividad.
```

---

No significa:

```text
Nunca fallar.
```

---

Significa:

```text
Recuperarse

rápidamente.
```

---

# Arquitectura

```text
Application

       │

       ▼

Load Balancer

       │

 ┌─────┴─────┐

 │           │

Primary   Standby

Database  Database
```

---

Si falla:

```text
Primary

↓

Standby

↓

Asume el servicio.
```

---

# Componentes

Una solución HA normalmente incluye:

```text
Servidor Primario

Servidor Secundario

Replicación

Monitoreo

Failover
```

---

# Servidor Primario

Recibe:

```text
Lecturas

Escrituras
```

---

Es el servidor principal.

---

# Servidor Secundario

Mantiene una copia sincronizada.

---

Puede utilizarse para:

```text
Failover

Lecturas

Backups
```

---

# Failover

Proceso automático o manual mediante el cual el servidor secundario se convierte en el nuevo servidor principal.

---

Ejemplo:

```text
Primary

↓

Falla

↓

Standby

↓

Nuevo Primary
```

---

# Failback

Cuando el servidor original vuelve a estar disponible.

---

Proceso:

```text
Servidor reparado

↓

Sincronización

↓

Regreso al servicio
```

---

# Objetivos

Una arquitectura HA busca:

```text
Reducir Downtime

↓

Reducir interrupciones

↓

Mantener disponibilidad
```

---

# Métricas

## Availability

Porcentaje de tiempo disponible.

Ejemplos:

```text
99%

99.9%

99.99%

99.999%
```

---

## Five Nines

```text
99.999%
```

---

Equivale aproximadamente a:

```text
5 minutos

de indisponibilidad

por año.
```

---

# Alta Disponibilidad vs Backup

## Backup

Protege datos.

---

## High Availability

Protege el servicio.

---

Ambos son necesarios.

---

# Alta Disponibilidad vs Disaster Recovery

HA:

```text
Recuperación rápida

↓

Fallas locales.
```

---

Disaster Recovery:

```text
Recuperación

↓

Ante desastres mayores.
```

---

# Caso Real

Empresa de Comercio Electrónico.

Arquitectura:

```text
Primary Database

↓

Streaming Replication

↓

Standby Database

↓

Automatic Failover
```

---

Si falla el servidor principal:

```text
La aplicación

continúa funcionando.
```

---

# Tecnologías Comunes

## PostgreSQL

```text
Streaming Replication

Patroni

Pgpool-II
```

---

## SQL Server

```text
Always On Availability Groups
```

---

## Oracle

```text
Oracle Data Guard

Oracle RAC
```

---

## MySQL

```text
Group Replication

InnoDB Cluster
```

---

# Beneficios

## Mayor disponibilidad

---

## Menor Downtime

---

## Continuidad del negocio

---

## Mayor confiabilidad

---

## Mejor experiencia para los usuarios

---

# Buenas Prácticas

## Monitorear continuamente

Detectar fallas rápidamente.

---

## Automatizar el Failover

Reducir tiempos de recuperación.

---

## Probar escenarios de falla

Validar el funcionamiento del entorno.

---

## Mantener la replicación sincronizada

Evitar pérdida de datos.

---

## Documentar procedimientos

Facilitar la operación.

---

# Error Común

Pensar que:

```text
Backup

↓

Es suficiente.
```

---

Problema:

```text
Restaurar

puede tardar

horas.
```

---

Mientras tanto:

```text
La aplicación

permanece

fuera de servicio.
```

---

# Error Conceptual Frecuente

Muchos creen:

```text
High Availability

=

No perder datos.
```

---

Incorrecto.

El objetivo principal es:

```text
Mantener

el servicio

disponible.
```

---

La protección de datos corresponde principalmente a:

```text
Backups

y

Disaster Recovery.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia

entre High Availability

y Backup?
```

---

Respuesta:

```text
Los Backups permiten recuperar información después de una pérdida de datos.

High Availability busca mantener la base de datos disponible mediante servidores redundantes, replicación y mecanismos de failover para minimizar el tiempo de inactividad.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Qué es un Failover?
```

---

Respuesta:

```text
Es el proceso mediante el cual un servidor secundario asume automáticamente o de forma manual el rol del servidor principal cuando este deja de estar disponible, permitiendo que la aplicación continúe operando con la menor interrupción posible.
```

---

# Pensamiento de un DBA

Antes de diseñar una arquitectura HA pregúntate:

1. ¿Cuál es el tiempo máximo de inactividad permitido?
2. ¿Necesito failover automático o manual?
3. ¿Qué nivel de disponibilidad requiere el negocio?
4. ¿Cómo monitorearé los servidores?
5. ¿Cómo probaré los escenarios de falla?
6. ¿Qué impacto tendrá una caída del servidor principal?
7. ¿Cómo realizaré el failback de forma segura?

---

# Relación con los siguientes módulos

```text
SQL INJECTION
        ↓
HIGH AVAILABILITY
        ↓
REPLICATION
        ↓
DISASTER RECOVERY
        ↓
DATABASE MONITORING
```

---

# Resumen

High Availability (HA) es el conjunto de estrategias utilizadas para mantener una base de datos disponible incluso cuando ocurre una falla.

Conceptos principales:

- Primary Database.
- Standby Database.
- Failover.
- Failback.
- Replicación.
- Disponibilidad.
- Downtime.

Beneficios:

- Mayor disponibilidad.
- Menor tiempo de inactividad.
- Continuidad del negocio.
- Mejor experiencia para los usuarios.
- Arquitecturas resilientes.

Una solución de High Availability bien diseñada permite que las aplicaciones continúen operando incluso frente a fallas de infraestructura, convirtiéndose en un componente esencial de cualquier entorno de producción.
