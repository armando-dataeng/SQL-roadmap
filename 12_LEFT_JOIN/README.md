# LEFT JOIN

## Definición

La cláusula `LEFT JOIN` permite combinar registros de dos tablas relacionadas.

A diferencia de `INNER JOIN`, `LEFT JOIN` conserva todas las filas de la tabla izquierda, incluso cuando no existe una coincidencia en la tabla derecha.

Cuando no existe coincidencia, SQL devuelve `NULL` en las columnas de la tabla derecha.

---

## Conceptos clave

LEFT JOIN responde a la pregunta:

> ¿Cómo puedo conservar todos los registros de la tabla principal aunque no tengan relación en la tabla secundaria?

Características:

- Conserva todas las filas de la tabla izquierda.
- Devuelve las coincidencias encontradas en la tabla derecha.
- Si no existe coincidencia, devuelve NULL.
- No modifica ninguna tabla.

---

## Sintaxis

```sql
SELECT columnas
FROM TablaA
LEFT JOIN TablaB
    ON TablaA.Columna = TablaB.Columna;
```

Ejemplo:

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
LEFT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Relación utilizada

### Tabla Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Juan |
| 2 | Ana |
| 3 | Pedro |

### Tabla Cuentas

| IdCuenta | NumeroCuenta | IdCliente |
|-----------|-------------|------------|
| 101 | 0001 | 1 |
| 102 | 0002 | 2 |

---

## Resultado

| Nombre | NumeroCuenta |
|---------|-------------|
| Juan | 0001 |
| Ana | 0002 |
| Pedro | NULL |

Pedro aparece porque LEFT JOIN conserva todas las filas de la tabla izquierda.

---

## Problema

Mostrar todos los clientes, tengan o no tengan cuenta bancaria.

### Datos

Tablas:

```text
Clientes
Cuentas
```

Relación:

```text
Clientes.IdCliente
=
Cuentas.IdCliente
```

### Lógica

Mostrar todos los clientes.

Si un cliente tiene cuenta:

```text
Mostrar la cuenta.
```

Si no tiene cuenta:

```text
Mostrar NULL.
```

### SQL

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
LEFT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Tabla izquierda y tabla derecha

En:

```sql
FROM Clientes c
LEFT JOIN Cuentas cu
```

Tabla izquierda:

```text
Clientes
```

Tabla derecha:

```text
Cuentas
```

LEFT JOIN siempre conserva las filas de la tabla izquierda.

---

## La cláusula ON

```sql
ON c.IdCliente = cu.IdCliente
```

SQL compara:

```text
Clientes.IdCliente
```

con

```text
Cuentas.IdCliente
```

Cuando son iguales:

```text
Une temporalmente las filas.
```

Cuando no son iguales:

```text
Conserva la fila izquierda y rellena con NULL.
```

---

## Casos de uso reales

### Clientes con o sin cuenta

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
LEFT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Caso:

```text
Detectar clientes que aún no poseen cuentas bancarias.
```

---

### Cuentas con o sin transacciones

```sql
SELECT
    cu.NumeroCuenta,
    t.Monto
FROM Cuentas cu
LEFT JOIN Transacciones t
    ON cu.IdCuenta = t.IdCuenta;
```

Caso:

```text
Identificar cuentas sin movimientos.
```

---

### Clientes y movimientos financieros

```sql
SELECT
    c.Nombre,
    t.Monto
FROM Clientes c
LEFT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente
LEFT JOIN Transacciones t
    ON cu.IdCuenta = t.IdCuenta;
```

Caso:

```text
Generar reportes completos de actividad financiera.
```

---

## Diferencia entre INNER JOIN y LEFT JOIN

### INNER JOIN

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Resultado:

```text
Juan
Ana
```

---

### LEFT JOIN

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
LEFT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Resultado:

```text
Juan
Ana
Pedro
```

Pedro aparece porque LEFT JOIN conserva todas las filas de la tabla izquierda.

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes c
LEFT JOIN Cuentas cu;
```

✔ Correcto

```sql
SELECT *
FROM Clientes c
LEFT JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
LEFT JOIN
```

devuelve los mismos resultados que:

```sql
INNER JOIN
```

Incorrecto.

LEFT JOIN conserva todas las filas de la tabla izquierda.

INNER JOIN conserva únicamente las coincidencias.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar LEFT JOIN pregúntate:

1. ¿Cuál es mi tabla principal?
2. ¿Necesito conservar todos sus registros?
3. ¿Qué ocurre cuando no existe coincidencia?
4. ¿Debo mostrar NULL para identificar datos faltantes?

### Relación entre conceptos

INNER JOIN responde:

> ¿Qué registros coinciden?

LEFT JOIN responde:

> ¿Qué registros existen en la tabla principal aunque no tengan coincidencia?

---

## Resumen

LEFT JOIN combina registros de dos tablas relacionadas.

Características principales:

- Conserva todas las filas de la tabla izquierda.
- Devuelve coincidencias de la tabla derecha.
- Utiliza NULL cuando no existe coincidencia.
- No modifica datos.
- Es uno de los JOINs más utilizados en sistemas reales.

Se utiliza frecuentemente para:

- Auditorías.
- Detección de datos faltantes.
- Reportes completos.
- Análisis de clientes sin actividad.
- Ingeniería de Datos.
