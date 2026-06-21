# CTE (Common Table Expression)

## Definición

Un CTE (Common Table Expression) es una consulta temporal nombrada que existe únicamente durante la ejecución de una sentencia SQL.

Se define utilizando la cláusula:

```sql
WITH
```

y permite dividir consultas complejas en bloques más legibles.

---

## Conceptos clave

Un CTE responde a la pregunta:

> ¿Cómo puedo dividir una consulta compleja en pasos más fáciles de leer?

Características:

- Mejora la legibilidad.
- Facilita el mantenimiento.
- Existe solo durante la ejecución.
- No crea tablas físicas.
- Puede reemplazar muchas subconsultas.

---

## Sintaxis

```sql
WITH NombreCTE AS
(
    SELECT columnas
    FROM tabla
)
SELECT *
FROM NombreCTE;
```

---

## Primer ejemplo

### Problema

Mostrar todos los clientes.

### SQL

```sql
WITH ClientesCTE AS
(
    SELECT *
    FROM Clientes
)
SELECT *
FROM ClientesCTE;
```

---

## ¿Qué hace SQL?

Paso 1:

```sql
SELECT *
FROM Clientes
```

Paso 2:

Guarda temporalmente el resultado como:

```text
ClientesCTE
```

Paso 3:

```sql
SELECT *
FROM ClientesCTE;
```

---

## Caso bancario

### Problema

Calcular el saldo total por cliente.

### SQL

```sql
WITH SaldoClientes AS
(
    SELECT
        IdCliente,
        SUM(Saldo) AS SaldoTotal
    FROM Cuentas
    GROUP BY IdCliente
)
SELECT *
FROM SaldoClientes;
```

---

## Resultado esperado

| IdCliente | SaldoTotal |
|------------|------------|
| 1 | 15000 |
| 2 | 8000 |
| 3 | 22000 |

---

## CTE vs Subquery

### Subquery

```sql
SELECT *
FROM
(
    SELECT
        IdCliente,
        SUM(Saldo) AS SaldoTotal
    FROM Cuentas
    GROUP BY IdCliente
) AS Resumen;
```

---

### CTE

```sql
WITH Resumen AS
(
    SELECT
        IdCliente,
        SUM(Saldo) AS SaldoTotal
    FROM Cuentas
    GROUP BY IdCliente
)
SELECT *
FROM Resumen;
```

---

## ¿Cuál es más legible?

Normalmente:

```text
CTE
```

porque separa claramente cada etapa de la consulta.

---

## Múltiples CTE

Podemos definir varios.

### SQL

```sql
WITH ClientesVIP AS
(
    SELECT
        IdCliente,
        SUM(Saldo) AS SaldoTotal
    FROM Cuentas
    GROUP BY IdCliente
),
ClientesPremium AS
(
    SELECT *
    FROM ClientesVIP
    WHERE SaldoTotal > 10000
)
SELECT *
FROM ClientesPremium;
```

---

## Caso real

### Clientes con más de 10,000

```sql
WITH SaldoClientes AS
(
    SELECT
        IdCliente,
        SUM(Saldo) AS SaldoTotal
    FROM Cuentas
    GROUP BY IdCliente
)
SELECT *
FROM SaldoClientes
WHERE SaldoTotal > 10000;
```

---

## JOIN con CTE

### SQL

```sql
WITH SaldoClientes AS
(
    SELECT
        IdCliente,
        SUM(Saldo) AS SaldoTotal
    FROM Cuentas
    GROUP BY IdCliente
)
SELECT
    c.Nombre,
    sc.SaldoTotal
FROM Clientes c
INNER JOIN SaldoClientes sc
    ON c.IdCliente = sc.IdCliente;
```

---

## Casos de uso reales

### Data Engineering

```sql
WITH TransaccionesDiarias AS
(
    SELECT
        FechaTransaccion,
        SUM(Monto) AS TotalDia
    FROM Transacciones
    GROUP BY FechaTransaccion
)
SELECT *
FROM TransaccionesDiarias;
```

---

### Business Intelligence

```sql
WITH VentasMensuales AS
(
    SELECT
        Mes,
        SUM(Ventas) AS TotalVentas
    FROM Ventas
    GROUP BY Mes
)
SELECT *
FROM VentasMensuales;
```

---

### Reporting

```sql
WITH ClientesActivos AS
(
    SELECT *
    FROM Clientes
    WHERE Activo = 1
)
SELECT *
FROM ClientesActivos;
```

---

## Error común

❌ Incorrecto

```sql
WITH ClientesCTE
SELECT *
FROM Clientes;
```

✔ Correcto

```sql
WITH ClientesCTE AS
(
    SELECT *
    FROM Clientes
)
SELECT *
FROM ClientesCTE;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```text
CTE crea una tabla
```

Incorrecto.

Un CTE:

```text
NO crea una tabla.
NO almacena datos permanentemente.
```

Existe únicamente durante la ejecución de la consulta.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar un CTE pregúntate:

1. ¿Mi consulta es difícil de leer?
2. ¿Tengo varias subconsultas anidadas?
3. ¿Puedo dividir la lógica en etapas?
4. ¿Necesito reutilizar un resultado temporal?

---

## Relación con otros conceptos

```text
SELECT       → Obtener datos
WHERE        → Filtrar datos
JOIN         → Relacionar tablas
GROUP BY     → Agrupar datos
HAVING       → Filtrar grupos
SUBQUERY     → Consulta dentro de otra consulta
CTE          → Consulta temporal nombrada
```

---

## CTE Recursivo

Los CTE también pueden ser recursivos.

Ejemplo:

```sql
WITH Numeros AS
(
    SELECT 1 AS Numero

    UNION ALL

    SELECT Numero + 1
    FROM Numeros
    WHERE Numero < 10
)
SELECT *
FROM Numeros;
```

Resultado:

```text
1
2
3
4
5
6
7
8
9
10
```

Muy utilizado para:

- Jerarquías
- Árboles
- Organigramas
- Estructuras padre-hijo

---

## Resumen

Los CTE permiten construir consultas complejas de forma clara y mantenible.

Ventajas:

- Mejor legibilidad.
- Mejor mantenimiento.
- Menos subconsultas anidadas.
- Muy utilizados en Data Engineering.
- Muy utilizados en Business Intelligence.

Son una de las herramientas más importantes del SQL moderno.
