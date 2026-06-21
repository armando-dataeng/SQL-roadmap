# GROUP BY

## Definición

La cláusula `GROUP BY` permite agrupar filas que comparten un mismo valor.

Se utiliza junto con funciones agregadas para resumir datos.

Es una de las herramientas más importantes para:

* Business Intelligence
* Data Analytics
* Data Engineering
* Reporting
* Dashboards

---

## Conceptos clave

GROUP BY responde a la pregunta:

> ¿Cómo puedo resumir información por categorías?

Ejemplos:

* Clientes por país
* Cuentas por tipo
* Transacciones por cliente
* Ventas por producto

---

## Sintaxis

```sql
SELECT columna,
       funcion_agregada()
FROM tabla
GROUP BY columna;
```

---

## Problema

¿Cuántas cuentas tiene cada cliente?

### Datos

Tabla:

```text
Cuentas
```

Columnas:

```text
IdCliente
IdCuenta
```

### Lógica

1. Agrupar por cliente.
2. Contar cuentas.

### SQL

```sql
SELECT
    IdCliente,
    COUNT(*) AS TotalCuentas
FROM Cuentas
GROUP BY IdCliente;
```

---

## Resultado esperado

| IdCliente | TotalCuentas |
| --------- | ------------ |
| 1         | 2            |
| 2         | 1            |
| 3         | 3            |

---

## GROUP BY con SUM

### Problema

¿Cuál es el saldo total por cliente?

### SQL

```sql
SELECT
    IdCliente,
    SUM(Saldo) AS SaldoTotal
FROM Cuentas
GROUP BY IdCliente;
```

---

## GROUP BY con AVG

### Problema

¿Cuál es el saldo promedio por cliente?

### SQL

```sql
SELECT
    IdCliente,
    AVG(Saldo) AS SaldoPromedio
FROM Cuentas
GROUP BY IdCliente;
```

---

## Casos de uso reales

### Transacciones por cuenta

```sql
SELECT
    IdCuenta,
    COUNT(*) AS TotalTransacciones
FROM Transacciones
GROUP BY IdCuenta;
```

---

### Saldo por tipo de cuenta

```sql
SELECT
    TipoCuenta,
    SUM(Saldo) AS SaldoTotal
FROM Cuentas
GROUP BY TipoCuenta;
```

---

## Error común

❌ Incorrecto

```sql
SELECT
    IdCliente,
    COUNT(*)
FROM Cuentas;
```

✔ Correcto

```sql
SELECT
    IdCliente,
    COUNT(*)
FROM Cuentas
GROUP BY IdCliente;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
GROUP BY
```

ordena datos.

Incorrecto.

GROUP BY agrupa.

Para ordenar se utiliza:

```sql
ORDER BY
```

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar GROUP BY pregúntate:

1. ¿Qué categoría quiero analizar?
2. ¿Qué métrica necesito calcular?
3. ¿Necesito contar?
4. ¿Necesito sumar?
5. ¿Necesito promediar?

---

## Resumen

GROUP BY permite agrupar registros para generar métricas y análisis.

Trabaja frecuentemente junto a:

* COUNT()
* SUM()
* AVG()
* MIN()
* MAX()
