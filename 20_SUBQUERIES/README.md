# SUBQUERIES

## Definición

Una Subquery (Subconsulta) es una consulta SQL anidada dentro de otra consulta SQL.

Permite utilizar el resultado de una consulta como entrada para otra.

También se conoce como:

- Nested Query
- Inner Query
- Subconsulta

---

## Conceptos clave

Una subconsulta responde a la pregunta:

> ¿Puedo utilizar el resultado de una consulta para construir otra consulta?

La respuesta es:

```text
Sí.
```

SQL ejecuta primero la subconsulta y luego utiliza ese resultado en la consulta principal.

---

## Sintaxis

```sql
SELECT columnas
FROM tabla
WHERE columna IN
(
    SELECT columna
    FROM tabla
);
```

---

## Ejemplo básico

### Problema

Mostrar los clientes que tienen cuentas bancarias.

### Datos

Tablas:

```text
Clientes
Cuentas
```

### Lógica

1. Obtener los IdCliente de la tabla Cuentas.
2. Buscar esos clientes en la tabla Clientes.

### SQL

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Cuentas
);
```

---

## ¿Qué ejecuta SQL primero?

Primero:

```sql
SELECT IdCliente
FROM Cuentas;
```

Resultado:

```text
1
2
3
```

Luego:

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN (1,2,3);
```

---

## Subquery en WHERE

Es el caso más común.

### Problema

Mostrar clientes con cuentas superiores a 10,000.

### SQL

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Cuentas
    WHERE Saldo > 10000
);
```

---

## Subquery con operadores de comparación

### Problema

Mostrar la cuenta con el saldo más alto.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo =
(
    SELECT MAX(Saldo)
    FROM Cuentas
);
```

---

## ¿Qué hace SQL?

Primero:

```sql
SELECT MAX(Saldo)
FROM Cuentas;
```

Resultado:

```text
95000
```

Después:

```sql
SELECT *
FROM Cuentas
WHERE Saldo = 95000;
```

---

## Subquery con AVG

### Problema

Mostrar cuentas cuyo saldo es superior al promedio.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE Saldo >
(
    SELECT AVG(Saldo)
    FROM Cuentas
);
```

---

## Casos de uso reales

### Clientes VIP

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Cuentas
    WHERE Saldo > 50000
);
```

---

### Transacciones superiores al promedio

```sql
SELECT *
FROM Transacciones
WHERE Monto >
(
    SELECT AVG(Monto)
    FROM Transacciones
);
```

---

### Cuenta con mayor saldo

```sql
SELECT *
FROM Cuentas
WHERE Saldo =
(
    SELECT MAX(Saldo)
    FROM Cuentas
);
```

---

## Subquery en FROM

Una subconsulta también puede utilizarse como tabla temporal.

### SQL

```sql
SELECT *
FROM
(
    SELECT
        IdCliente,
        SUM(Saldo) AS SaldoTotal
    FROM Cuentas
    GROUP BY IdCliente
) AS ResumenClientes;
```

---

## Subquery en SELECT

También es posible.

### SQL

```sql
SELECT
    Nombre,
    (
        SELECT COUNT(*)
        FROM Cuentas
        WHERE Cuentas.IdCliente = Clientes.IdCliente
    ) AS TotalCuentas
FROM Clientes;
```

---

## Tipos de Subqueries

### Single Row

Devuelven una sola fila.

```sql
SELECT MAX(Saldo)
FROM Cuentas;
```

---

### Multiple Row

Devuelven varias filas.

```sql
SELECT IdCliente
FROM Cuentas;
```

---

### Correlated Subquery

Dependen de la consulta principal.

```sql
SELECT *
FROM Clientes c
WHERE EXISTS
(
    SELECT 1
    FROM Cuentas cu
    WHERE cu.IdCliente = c.IdCliente
);
```

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes
WHERE IdCliente =
(
    SELECT IdCliente
    FROM Cuentas
);
```

Si la subconsulta devuelve varias filas:

```text
Error
```

---

✔ Correcto

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Cuentas
);
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```text
JOIN reemplaza Subqueries
```

o

```text
Subqueries reemplazan JOIN
```

Incorrecto.

Ambas herramientas tienen usos distintos.

En muchos casos:

```sql
JOIN
```

es más eficiente.

En otros:

```sql
Subquery
```

es más legible.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar una subconsulta pregúntate:

1. ¿Necesito el resultado de una consulta dentro de otra?
2. ¿La subconsulta devuelve una fila o varias?
3. ¿Debo utilizar IN, EXISTS o = ?
4. ¿Un JOIN sería más eficiente?
5. ¿La consulta seguirá siendo legible?

---

## Relación con otros conceptos

```text
SELECT            → Obtener datos
WHERE             → Filtrar datos
JOIN              → Relacionar tablas
GROUP BY          → Agrupar datos
HAVING            → Filtrar grupos
SUBQUERY          → Utilizar una consulta dentro de otra
```

---

## Resumen

Las Subqueries permiten construir consultas más complejas utilizando el resultado de otras consultas.

Principales ubicaciones:

- WHERE
- FROM
- SELECT

Son ampliamente utilizadas en:

- Business Intelligence
- Data Analytics
- Data Engineering
- SQL Server
- PostgreSQL
- MySQL
- Oracle

Constituyen uno de los fundamentos del SQL intermedio y avanzado.
