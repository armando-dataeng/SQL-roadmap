# EXISTS, IN y NOT IN

## Definición

EXISTS, IN y NOT IN son operadores utilizados para trabajar con subconsultas.

Permiten verificar:

- Si un valor pertenece a un conjunto.
- Si un valor no pertenece a un conjunto.
- Si existen registros relacionados.

Son ampliamente utilizados en:

- SQL Intermedio
- SQL Avanzado
- Data Engineering
- Business Intelligence
- Reporting

---

# IN

## Definición

IN permite verificar si un valor existe dentro de una lista o conjunto de resultados.

---

## Sintaxis

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN (1,2,3);
```

---

## Problema

Mostrar clientes que poseen cuentas.

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

## ¿Qué hace SQL?

Primero ejecuta:

```sql
SELECT IdCliente
FROM Cuentas;
```

Supongamos:

```text
1
2
3
```

Luego ejecuta:

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN (1,2,3);
```

---

## Caso real

Clientes con cuentas activas.

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Cuentas
    WHERE Estado = 'Activa'
);
```

---

# NOT IN

## Definición

NOT IN permite obtener registros que NO pertenecen a un conjunto.

---

## Sintaxis

```sql
SELECT *
FROM Clientes
WHERE IdCliente NOT IN (1,2,3);
```

---

## Problema

Mostrar clientes que no tienen cuentas.

### SQL

```sql
SELECT *
FROM Clientes
WHERE IdCliente NOT IN
(
    SELECT IdCliente
    FROM Cuentas
);
```

---

## Resultado

Devuelve únicamente clientes sin cuentas asociadas.

---

## Caso real

Clientes sin movimientos bancarios.

```sql
SELECT *
FROM Clientes
WHERE IdCliente NOT IN
(
    SELECT IdCliente
    FROM Transacciones
);
```

---

# EXISTS

## Definición

EXISTS verifica si la subconsulta devuelve al menos una fila.

No le interesan los valores.

Solo verifica existencia.

---

## Sintaxis

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

## ¿Qué significa?

Para cada cliente:

```text
¿Existe al menos una cuenta?
```

Si existe:

```text
TRUE
```

Si no existe:

```text
FALSE
```

---

## Caso bancario

Clientes con cuentas.

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

# NOT EXISTS

## Definición

Es el opuesto de EXISTS.

Devuelve filas cuando NO existe una coincidencia.

---

## Problema

Clientes sin cuentas.

### SQL

```sql
SELECT *
FROM Clientes c
WHERE NOT EXISTS
(
    SELECT 1
    FROM Cuentas cu
    WHERE cu.IdCliente = c.IdCliente
);
```

---

# EXISTS vs IN

## IN

```sql
SELECT *
FROM Clientes
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Cuentas
);
```

Pregunta:

```text
¿El IdCliente pertenece a este conjunto?
```

---

## EXISTS

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

Pregunta:

```text
¿Existe una fila relacionada?
```

---

# ¿Cuál es más rápido?

En conjuntos pequeños:

```text
Diferencia mínima.
```

En conjuntos grandes:

```text
EXISTS suele ser más eficiente.
```

Porque SQL puede detener la búsqueda al encontrar la primera coincidencia.

---

# Error común

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
Error.
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

# Error conceptual frecuente

Muchos principiantes creen que:

```text
EXISTS devuelve datos.
```

Incorrecto.

EXISTS devuelve:

```text
TRUE o FALSE
```

dependiendo de si existen filas.

---

# Pensamiento de Ingeniería de Datos

Antes de utilizar estos operadores pregúntate:

1. ¿Necesito verificar pertenencia?
2. ¿Necesito verificar existencia?
3. ¿La subconsulta devuelve muchas filas?
4. ¿Necesito máximo rendimiento?
5. ¿EXISTS sería más eficiente que IN?

---

# Resumen

IN

```text
Verifica pertenencia.
```

NOT IN

```text
Verifica ausencia.
```

EXISTS

```text
Verifica existencia.
```

NOT EXISTS

```text
Verifica no existencia.
```

Son herramientas fundamentales para:

- Subconsultas
- Data Engineering
- Business Intelligence
- SQL Server
- PostgreSQL
- MySQL
- Oracle
