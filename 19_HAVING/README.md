# HAVING

## Definición

La cláusula `HAVING` permite filtrar grupos creados por GROUP BY.

Mientras que WHERE filtra filas individuales, HAVING filtra grupos completos.

---

## Conceptos clave

HAVING responde a la pregunta:

> ¿Qué grupos cumplen una condición?

---

## Diferencia entre WHERE y HAVING

### WHERE

Filtra filas.

```sql
SELECT *
FROM Cuentas
WHERE Saldo > 1000;
```

---

### HAVING

Filtra grupos.

```sql
SELECT
    IdCliente,
    SUM(Saldo)
FROM Cuentas
GROUP BY IdCliente
HAVING SUM(Saldo) > 10000;
```

---

## Sintaxis

```sql
SELECT columna,
       funcion_agregada()
FROM tabla
GROUP BY columna
HAVING condicion;
```

---

## Problema

Mostrar clientes cuyo saldo total supera los 10,000.

### Datos

Tabla:

```text
Cuentas
```

### Lógica

1. Agrupar por cliente.
2. Sumar saldos.
3. Mostrar únicamente quienes superan 10,000.

### SQL

```sql
SELECT
    IdCliente,
    SUM(Saldo) AS SaldoTotal
FROM Cuentas
GROUP BY IdCliente
HAVING SUM(Saldo) > 10000;
```

---

## Casos de uso reales

### Clientes con más de una cuenta

```sql
SELECT
    IdCliente,
    COUNT(*) AS TotalCuentas
FROM Cuentas
GROUP BY IdCliente
HAVING COUNT(*) > 1;
```

---

### Cuentas con muchas transacciones

```sql
SELECT
    IdCuenta,
    COUNT(*) AS TotalMovimientos
FROM Transacciones
GROUP BY IdCuenta
HAVING COUNT(*) > 100;
```

---

### Clientes con alto saldo

```sql
SELECT
    IdCliente,
    SUM(Saldo) AS SaldoTotal
FROM Cuentas
GROUP BY IdCliente
HAVING SUM(Saldo) > 50000;
```

---

## Error común

❌ Incorrecto

```sql
SELECT
    IdCliente,
    SUM(Saldo)
FROM Cuentas
HAVING SUM(Saldo) > 10000;
```

✔ Correcto

```sql
SELECT
    IdCliente,
    SUM(Saldo)
FROM Cuentas
GROUP BY IdCliente
HAVING SUM(Saldo) > 10000;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
WHERE SUM(Saldo) > 10000
```

es válido.

Incorrecto.

WHERE no puede filtrar resultados agregados.

Para eso existe:

```sql
HAVING
```

---

## Orden lógico de ejecución

SQL procesa:

```text
FROM
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar HAVING pregúntate:

1. ¿Estoy trabajando con grupos?
2. ¿Necesito filtrar una agregación?
3. ¿La condición depende de COUNT, SUM o AVG?
4. ¿Debo usar WHERE o HAVING?

---

## Resumen

HAVING filtra grupos creados por GROUP BY.

WHERE filtra filas.

HAVING filtra grupos.

Es una herramienta fundamental para:

* Dashboards
* KPIs
* Business Intelligence
* Data Analytics
* Data Engineering
* Reporting
