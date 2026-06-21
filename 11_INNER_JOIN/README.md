# INNER JOIN

## Definición

La cláusula `INNER JOIN` permite combinar filas de dos o más tablas relacionadas.

Solo devuelve los registros que cumplen la condición especificada en la cláusula `ON`.

Si no existe coincidencia entre las tablas, el registro no aparece en el resultado.

---

## Conceptos clave

INNER JOIN responde a la pregunta:

> ¿Qué registros tienen relación entre sí?

INNER JOIN es el mecanismo principal para relacionar tablas dentro de una base de datos relacional.

Se basa en:

- Claves primarias (PK)
- Claves foráneas (FK)
- Relaciones entre tablas

---

## Sintaxis

```sql
SELECT columnas
FROM TablaA
INNER JOIN TablaB
    ON TablaA.Columna = TablaB.Columna;
```

Ejemplo:

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
INNER JOIN Cuentas cu
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

```text
Juan   | 0001
Ana    | 0002
```

Pedro no aparece porque no tiene cuenta asociada.

---

## Problema

Mostrar el nombre del cliente y el número de cuenta asociado.

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

Relacionar cada cliente con sus cuentas utilizando el campo IdCliente.

### SQL

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Alias de tablas

Los alias permiten escribir consultas más legibles.

Ejemplo:

```sql
FROM Clientes c
```

Alias:

```text
c
```

---

```sql
FROM Cuentas cu
```

Alias:

```text
cu
```

Por lo tanto:

```sql
c.Nombre
```

significa:

```text
Nombre de la tabla Clientes
```

---

```sql
cu.NumeroCuenta
```

significa:

```text
NumeroCuenta de la tabla Cuentas
```

---

## La cláusula ON

La cláusula ON define la condición de unión.

Ejemplo:

```sql
ON c.IdCliente = cu.IdCliente
```

### ¿Qué hace SQL?

Compara:

```text
Clientes.IdCliente
```

con

```text
Cuentas.IdCliente
```

Cuando ambos valores son iguales:

```text
Une temporalmente las filas.
```

---

## Casos de uso reales

### Clientes y cuentas

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

Caso:

```text
Identificar el propietario de cada cuenta bancaria.
```

---

### Cuentas y transacciones

```sql
SELECT
    cu.NumeroCuenta,
    t.Monto
FROM Cuentas cu
INNER JOIN Transacciones t
    ON cu.IdCuenta = t.IdCuenta;
```

Caso:

```text
Visualizar movimientos asociados a una cuenta.
```

---

### Clientes y transacciones

```sql
SELECT
    c.Nombre,
    t.Monto
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente
INNER JOIN Transacciones t
    ON cu.IdCuenta = t.IdCuenta;
```

Caso:

```text
Analizar movimientos financieros por cliente.
```

---

## Error común

❌ Incorrecto

```sql
SELECT *
FROM Clientes c
INNER JOIN Cuentas cu;
```

✔ Correcto

```sql
SELECT *
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Error conceptual frecuente

Muchos principiantes creen que:

```sql
ON c.IdCliente = cu.IdCliente
```

copia valores de una tabla a otra.

Incorrecto.

INNER JOIN no modifica tablas.

INNER JOIN únicamente relaciona datos durante la ejecución de la consulta.

---

## Pensamiento de Ingeniería de Datos

Antes de utilizar INNER JOIN pregúntate:

1. ¿Qué tablas necesito relacionar?
2. ¿Cuál es la clave primaria?
3. ¿Cuál es la clave foránea?
4. ¿Qué relación existe entre ambas tablas?

### Relación entre conceptos

SELECT responde:

> ¿Qué información necesito obtener?

FROM responde:

> ¿De dónde obtendré la información?

WHERE responde:

> ¿Qué registros necesito?

INNER JOIN responde:

> ¿Qué registros están relacionados entre sí?

---

## Resumen

INNER JOIN permite combinar registros de múltiples tablas.

Características principales:

- Solo devuelve coincidencias.
- Utiliza relaciones entre tablas.
- Se apoya en claves primarias y foráneas.
- No modifica datos.
- Une filas temporalmente durante la consulta.

Es una de las herramientas más importantes de SQL y la base de los sistemas relacionales modernos.
