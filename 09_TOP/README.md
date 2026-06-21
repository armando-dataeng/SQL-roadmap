# TOP

## Definición

La cláusula `TOP` permite limitar la cantidad de filas devueltas por una consulta.

Es ampliamente utilizada para:

- Consultas rápidas
- Reportes
- Dashboards
- Paginación
- Análisis exploratorio

TOP es una característica propia de SQL Server.

---

## Conceptos clave

TOP responde a la pregunta:

> ¿Cuántos registros necesito obtener?

Sin TOP, SQL devuelve todos los registros que cumplen la consulta.

Con TOP, SQL devuelve únicamente la cantidad especificada.

---

## Sintaxis

```sql
SELECT TOP cantidad
columnas
FROM tabla;
```

Ejemplo:

```sql
SELECT TOP 5 *
FROM Clientes;
```

---

## Mostrar los primeros 5 clientes

### Problema

Mostrar únicamente los primeros 5 clientes registrados.

### Datos

Tabla:

```text
Clientes
```

### Lógica

Limitar el resultado a cinco registros.

### SQL

```sql
SELECT TOP 5 *
FROM Clientes;
```

---

## Mostrar las primeras 10 cuentas

### Problema

Mostrar únicamente las primeras 10 cuentas.

### Datos

Tabla:

```text
Cuentas
```

### Lógica

Limitar el resultado a diez registros.

### SQL

```sql
SELECT TOP 10 *
FROM Cuentas;
```

---

## Casos de uso reales

### Obtener los primeros clientes

```sql
SELECT TOP 10 *
FROM Clientes;
```

Caso:

```text
Inspeccionar rápidamente datos de clientes.
```

---

### Mostrar cuentas con mayor saldo

```sql
SELECT TOP 5 *
FROM Cuentas
ORDER BY Saldo DESC;
```

Caso:

```text
Identificar los clientes con mayor patrimonio.
```

---

### Mostrar transacciones recientes

```sql
SELECT TOP 20 *
FROM Transacciones
ORDER BY FechaTransaccion DESC;
```

Caso:

```text
Visualizar los últimos movimientos financieros.
```

---

### Mostrar usuarios más recientes

```sql
SELECT TOP 10 *
FROM Usuarios
ORDER BY FechaCreacion DESC;
```

Caso:

```text
Auditar nuevas cuentas del sistema.
```

---

## TOP con ORDER BY

Una práctica recomendada es utilizar TOP junto con ORDER BY.

Ejemplo:

```sql
SELECT TOP 5 *
FROM Cuentas
ORDER BY Saldo DESC;
```

### Lógica

1. Ordenar por saldo.
2. Obtener los primeros cinco registros.

Resultado:

```text
Las cinco cuentas con mayor saldo.
```

---

## TOP con porcentaje

SQL Server permite utilizar porcentajes.

Ejemplo:

```sql
SELECT TOP 10 PERCENT *
FROM Clientes;
```

### Lógica

Recuperar el 10% de los registros de la tabla.

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes
TOP 5;
```

✔ Correcto

```sql
SELECT TOP 5 *
FROM Clientes;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
SELECT TOP 5 *
FROM Clientes;
```

obtiene siempre los mismos registros.

Incorrecto.

Sin ORDER BY:

```sql
SELECT TOP 5 *
FROM Clientes;
```

SQL Server no garantiza qué cinco filas devolverá.

La forma correcta es:

```sql
SELECT TOP 5 *
FROM Clientes
ORDER BY IdCliente;
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar TOP pregúntate:

1. ¿Necesito todos los registros?
2. ¿Cuántos registros necesito realmente?
3. ¿Cuál es el criterio para elegirlos?
4. ¿Debo utilizar ORDER BY?

### Relación entre conceptos

SELECT responde:

> ¿Qué información necesito obtener?

FROM responde:

> ¿De dónde obtendré esa información?

WHERE responde:

> ¿Qué registros necesito?

ORDER BY responde:

> ¿Cómo quiero visualizar esos registros?

TOP responde:

> ¿Cuántos registros necesito devolver?

---

## Resumen

TOP permite limitar la cantidad de filas devueltas por una consulta.

Características principales:

- Disponible en SQL Server.
- Reduce la cantidad de registros retornados.
- Funciona mejor junto con ORDER BY.
- Puede utilizar cantidades fijas.
- Puede utilizar porcentajes.

Es ampliamente utilizado para:

- Reportes
- Dashboards
- Paginación
- Consultas exploratorias
- Análisis financiero
