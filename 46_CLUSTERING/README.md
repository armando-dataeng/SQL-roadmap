# CLUSTERING

## Definición

Database Clustering es una arquitectura en la que múltiples servidores trabajan juntos como un único sistema para proporcionar alta disponibilidad, escalabilidad y tolerancia a fallos.

El objetivo es garantizar que la base de datos continúe funcionando incluso si uno o más nodos dejan de estar disponibles.

---

# ¿Por qué existe?

Supongamos una empresa que recibe millones de transacciones al día.

Pregunta:

```text
¿Qué ocurre

si un único servidor

no puede manejar

toda la carga?
```

---

O peor aún:

```text
¿Qué ocurre

si ese servidor

falla?
```

---

La solución es:

```text
Clustering.
```

---

# Concepto Fundamental

Un Cluster está compuesto por:

```text
Varios servidores

↓

Trabajando

↓

Como un solo sistema.
```

---

Los usuarios normalmente no saben:

```text
Qué servidor

está respondiendo.
```

---

# Arquitectura

```text
Application

      │

      ▼

Load Balancer

      │

 ┌────┼────┐

 │    │    │

Node1 Node2 Node3

      │

 Shared Storage
```

---

Cada nodo puede atender solicitudes.

---

# Componentes

## Nodos

Son los servidores que forman el Cluster.

---

## Load Balancer

Distribuye las conexiones entre los nodos.

---

## Shared Storage

Algunos clusters utilizan almacenamiento compartido.

Otros utilizan replicación distribuida.

---

## Heartbeat

Permite verificar si un nodo continúa disponible.

---

Si un nodo deja de responder:

```text
Heartbeat

↓

Detecta la falla.
```

---

# Failover

Cuando un nodo falla:

```text
Node 1

↓

Falla

↓

Node 2

↓

Continúa operando.
```

---

El usuario normalmente no percibe la transición.

---

# Escalabilidad

Si aumenta la carga:

```text
Agregar

↓

Otro nodo.
```

---

El Cluster continúa funcionando.

---

# Tipos de Clustering

## Active-Passive

Solo un nodo atiende solicitudes.

El otro permanece en espera.

---

Arquitectura

```text
Primary

↓

Standby
```

---

Ventajas:

- Simple.
- Fácil administración.

---

## Active-Active

Todos los nodos procesan solicitudes.

---

Arquitectura

```text
Node 1

↓

Node 2

↓

Node 3
```

---

Ventajas:

- Mejor utilización de recursos.
- Mayor escalabilidad.

---

# Tecnologías

## Oracle

```text
Oracle RAC
```

Permite múltiples nodos activos.

---

## SQL Server

```text
Failover Cluster Instances
```

---

## PostgreSQL

Generalmente combina:

```text
Patroni

etcd

HAProxy
```

---

## MySQL

```text
InnoDB Cluster

MySQL NDB Cluster
```

---

# Clustering vs Replication

## Replication

```text
Copia datos.
```

---

## Clustering

```text
Coordina

varios servidores

como un único sistema.
```

---

La replicación puede formar parte del Cluster.

---

# Clustering vs High Availability

High Availability:

```text
Objetivo.
```

---

Clustering:

```text
Tecnología

para lograr

ese objetivo.
```

---

# Beneficios

## Alta disponibilidad

---

## Escalabilidad horizontal

---

## Tolerancia a fallos

---

## Balanceo de carga

---

## Continuidad del negocio

---

# Caso Real

Banco Internacional.

Arquitectura:

```text
Oracle RAC

↓

4 nodos activos

↓

Balanceador

↓

Aplicaciones
```

---

Si un nodo falla:

```text
Los demás

continúan

procesando

transacciones.
```

---

# Buenas Prácticas

## Monitorear todos los nodos

---

## Probar Failover

Regularmente.

---

## Sincronizar configuraciones

Todos los nodos deben ser consistentes.

---

## Supervisar el almacenamiento

Especialmente en arquitecturas compartidas.

---

## Documentar procedimientos

Facilita la recuperación.

---

# Error Común

Pensar que:

```text
Replication

=

Cluster.
```

---

Incorrecto.

La replicación sincroniza datos.

El Cluster coordina múltiples servidores.

---

# Error Conceptual Frecuente

Muchos creen:

```text
Agregar

más nodos

↓

Siempre mejora

el rendimiento.
```

---

Incorrecto.

También aumentan:

```text
Complejidad

Costos

Latencia

Administración
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es

un Database Cluster?
```

---

Respuesta:

```text
Es una arquitectura donde múltiples servidores trabajan como un único sistema para proporcionar alta disponibilidad, escalabilidad y tolerancia a fallos, permitiendo que la base de datos continúe operando incluso cuando uno de los nodos deja de estar disponible.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Cuál es la diferencia

entre Clustering

y Replication?
```

---

Respuesta:

```text
La replicación copia y sincroniza datos entre servidores.

El clustering coordina varios servidores para que funcionen como un único sistema, proporcionando alta disponibilidad y, en muchos casos, balanceo de carga.

Muchas soluciones de clustering utilizan replicación internamente.
```

---

# Pensamiento de un DBA

Antes de implementar un Cluster pregúntate:

1. ¿Cuál es el nivel de disponibilidad requerido?
2. ¿Necesito Active-Passive o Active-Active?
3. ¿Cómo se realizará el balanceo de carga?
4. ¿Cómo detectaré la caída de un nodo?
5. ¿Qué estrategia de almacenamiento utilizaré?
6. ¿Cómo probaré el failover?
7. ¿Cómo escalará el Cluster en el futuro?

---

# Relación con los siguientes módulos

```text
REPLICATION
        ↓
CLUSTERING
        ↓
DISASTER RECOVERY
        ↓
DATABASE MONITORING
        ↓
DATABASE MAINTENANCE
```

---

# Resumen

Database Clustering permite que múltiples servidores trabajen como un único sistema para mejorar la disponibilidad, la escalabilidad y la tolerancia a fallos.

Conceptos principales:

- Nodos.
- Load Balancer.
- Heartbeat.
- Failover.
- Active-Active.
- Active-Passive.

Beneficios:

- Alta disponibilidad.
- Balanceo de carga.
- Escalabilidad horizontal.
- Continuidad del negocio.
- Resiliencia frente a fallos.

El clustering es una de las arquitecturas más utilizadas en entornos empresariales donde la disponibilidad de la base de datos es un requisito crítico.
