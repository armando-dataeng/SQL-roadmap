# WINDOW FUNCTIONS

## Definición

Las Window Functions (Funciones de Ventana) permiten realizar cálculos sobre un conjunto de filas relacionadas sin agruparlas en una sola fila.

A diferencia de:

```sql
GROUP BY
```

las Window Functions conservan todas las filas originales.

---

## Conceptos clave

Las Window Functions responden preguntas como:

- ¿Cuál es el ranking de cada cliente?
- ¿Cuál fue la transacción anterior?
- ¿Cuál será la siguiente transacción?
- ¿Cuál es el saldo acumulado?
- ¿Cuál es el promedio por grupo?

---

## Sintaxis General

```sql
SELECT
    columna,
    Funcion() OVER(...)
FROM tabla;
```

La palabra clave más importante es:

```sql
OVER()
```

Porque define la ventana de datos sobre la que trabajará la función.

---

# OVER()

## Definición

OVER() define el conjunto de filas que utilizará la función.

Ejemplo:

```sql
SELECT
    Nombre,
    Saldo,
    ROW_NUMBER() OVER(
        ORDER BY Saldo DESC
    ) AS Ranking
FROM Clientes;
```

---

# ROW_NUMBER()

## Definición

Asigna un número único a cada fila.

---

## Problema

Numerar clientes por saldo.

### SQL

```sql
SELECT
    Nombre,
    Saldo,
    ROW_NUMBER() OVER(
        ORDER BY Saldo DESC
    ) AS Ranking
FROM Clientes;
```

---

## Resultado

| Nombre | Saldo | Ranking |
|----------|--------|----------|
| Ana | 10000 | 1 |
| Juan | 8000 | 2 |
| Pedro | 5000 | 3 |

---

## Caso real

Top clientes del banco.

---

# RANK()

## Definición

Asigna posiciones considerando empates.

---

## SQL

```sql
SELECT
    Nombre,
    Saldo,
    RANK() OVER(
        ORDER BY Saldo DESC
    ) AS Ranking
FROM Clientes;
```

---

## Resultado

| Nombre | Saldo | Ranking |
|----------|--------|----------|
| Ana | 10000 | 1 |
| Juan | 8000 | 2 |
| Pedro | 8000 | 2 |
| Luis | 5000 | 4 |

Observa:

```text
Se salta el número 3.
```

---

# DENSE_RANK()

## Definición

Similar a RANK(), pero sin saltos.

---

## SQL

```sql
SELECT
    Nombre,
    Saldo,
    DENSE_RANK() OVER(
        ORDER BY Saldo DESC
    ) AS Ranking
FROM Clientes;
```

---

## Resultado

| Nombre | Saldo | Ranking |
|----------|--------|----------|
| Ana | 10000 | 1 |
| Juan | 8000 | 2 |
| Pedro | 8000 | 2 |
| Luis | 5000 | 3 |

---

# LAG()

## Definición

Obtiene el valor de la fila anterior.

---

## Problema

Comparar cada transacción con la anterior.

### SQL

```sql
SELECT
    FechaTransaccion,
    Monto,
    LAG(Monto) OVER(
        ORDER BY FechaTransaccion
    ) AS MontoAnterior
FROM Transacciones;
```

---

## Resultado

| Fecha | Monto | MontoAnterior |
|---------|---------|---------------|
| 01/01 | 100 | NULL |
| 02/01 | 200 | 100 |
| 03/01 | 150 | 200 |

---

## Caso real

Análisis de tendencias.

---

# LEAD()

## Definición

Obtiene el valor de la siguiente fila.

---

## SQL

```sql
SELECT
    FechaTransaccion,
    Monto,
    LEAD(Monto) OVER(
        ORDER BY FechaTransaccion
    ) AS MontoSiguiente
FROM Transacciones;
```

---

## Resultado

| Fecha | Monto | MontoSiguiente |
|---------|---------|----------------|
| 01/01 | 100 | 200 |
| 02/01 | 200 | 150 |
| 03/01 | 150 | NULL |

---

## Caso real

Proyecciones y comparaciones.

---

# SUM() OVER()

## Definición

Permite realizar sumas acumuladas.

---

## Problema

Calcular saldo acumulado.

### SQL

```sql
SELECT
    FechaTransaccion,
    Monto,
    SUM(Monto) OVER(
        ORDER BY FechaTransaccion
    ) AS SaldoAcumulado
FROM Transacciones;
```

---

## Resultado

| Fecha | Monto | SaldoAcumulado |
|---------|---------|---------------|
| 01/01 | 100 | 100 |
| 02/01 | 200 | 300 |
| 03/01 | 150 | 450 |

---

# PARTITION BY

## Definición

Divide la ventana en grupos.

---

## SQL

```sql
SELECT
    IdCliente,
    Saldo,
    ROW_NUMBER() OVER(
        PARTITION BY IdCliente
        ORDER BY Saldo DESC
    ) AS Ranking
FROM Cuentas;
```

---

## ¿Qué hace?

Reinicia la numeración para cada cliente.

---

# Casos de uso reales

## Top clientes por saldo

```sql
SELECT
    Nombre,
    Saldo,
    RANK() OVER(
        ORDER BY Saldo DESC
    ) AS Ranking
FROM Clientes;
```

---

## Saldo acumulado

```sql
SELECT
    FechaTransaccion,
    SUM(Monto) OVER(
        ORDER BY FechaTransaccion
    )
FROM Transacciones;
```

---

## Comparación contra transacción anterior

```sql
SELECT
    Monto,
    LAG(Monto) OVER(
        ORDER BY FechaTransaccion
    )
FROM Transacciones;
```

---

# Error común

❌ Incorrecto

```sql
SELECT
    ROW_NUMBER()
FROM Clientes;
```

✔ Correcto

```sql
SELECT
    ROW_NUMBER() OVER(
        ORDER BY IdCliente
    )
FROM Clientes;
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```sql
GROUP BY
```

y

```sql
WINDOW FUNCTIONS
```

son lo mismo.

Incorrecto.

GROUP BY:

```text
Agrupa filas y reduce resultados.
```

Window Functions:

```text
Mantienen todas las filas originales.
```

---

# Pensamiento de Ingeniería de Datos

Antes de utilizar Window Functions pregúntate:

1. ¿Necesito conservar todas las filas?
2. ¿Necesito rankings?
3. ¿Necesito acumulados?
4. ¿Necesito comparar filas consecutivas?
5. ¿Necesito particionar datos?

---

# Relación con otros conceptos

```text
GROUP BY        → Agrupa filas
SUBQUERY        → Consulta dentro de consulta
CTE             → Consulta temporal nombrada
WINDOW FUNCTION → Analiza filas sin agruparlas
```

---

# Resumen

Funciones más importantes:

```sql
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
SUM() OVER()
AVG() OVER()
```

Son fundamentales para:

- Data Engineering
- Business Intelligence
- Reporting
- Dashboards
- SQL Avanzado
- Analítica Financiera
- Ciencia de Datos
