# QUERY OPTIMIZATION

## Definición

Query Optimization (Optimización de Consultas) es el proceso de escribir consultas SQL que consuman menos:

- CPU
- Memoria
- Disco
- Tiempo de ejecución

El objetivo es obtener los mismos resultados utilizando menos recursos.

---

## Conceptos clave

La optimización responde a la pregunta:

> ¿Cómo puedo obtener los mismos datos de forma más eficiente?

Una consulta correcta:

```sql
SELECT *
FROM Clientes;
```

No necesariamente es una consulta eficiente.

---

# ¿Por qué optimizar?

Supongamos:

Tabla:

```text
Clientes
```

Cantidad:

```text
10 filas
```

Consulta:

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 1;
```

Rápida.

---

Ahora:

```text
100 millones de filas
```

La misma consulta puede tardar segundos o minutos.

---

# Principio #1

## Evitar SELECT *

❌ Incorrecto

```sql
SELECT *
FROM Clientes;
```

Problema:

```text
Lee todas las columnas.
```

---

✔ Correcto

```sql
SELECT
    IdCliente,
    Nombre
FROM Clientes;
```

Beneficio:

```text
Menos datos.
Menos memoria.
Menos I/O.
```

---

# Principio #2

## Filtrar lo antes posible

❌ Menos eficiente

```sql
SELECT *
FROM Clientes;
```

---

✔ Más eficiente

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 1;
```

Beneficio:

```text
Menos filas procesadas.
```

---

# Principio #3

## Utilizar índices correctamente

Consulta:

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 100;
```

Índice:

```sql
CREATE INDEX IX_Clientes_Id
ON Clientes(IdCliente);
```

Resultado:

```text
Index Seek
```

en lugar de:

```text
Table Scan
```

---

# Principio #4

## Evitar funciones sobre columnas indexadas

❌ Incorrecto

```sql
SELECT *
FROM Clientes
WHERE YEAR(FechaRegistro) = 2025;
```

Problema:

```text
SQL no puede utilizar correctamente el índice.
```

---

✔ Correcto

```sql
SELECT *
FROM Clientes
WHERE FechaRegistro >= '2025-01-01'
AND FechaRegistro < '2026-01-01';
```

Beneficio:

```text
Permite Index Seek.
```

---

# Principio #5

## Evitar cálculos innecesarios

❌

```sql
SELECT
    Saldo * 1.15
FROM Cuentas;
```

si el cálculo no es necesario.

---

Cada operación:

```text
Consume CPU.
```

---

# Principio #6

## Utilizar EXISTS en lugar de IN cuando corresponda

Muchas veces:

```sql
EXISTS
```

es más eficiente.

---

Ejemplo:

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

# Principio #7

## Evitar cursores

❌

```sql
CURSOR
```

fila por fila.

---

✔

```sql
Operaciones basadas en conjuntos.
```

---

SQL está diseñado para procesar:

```text
Conjuntos de datos.
```

No registros individuales.

---

# Principio #8

## Utilizar JOIN correctamente

❌

```sql
SELECT *
FROM Clientes c,
     Cuentas cu;
```

---

✔

```sql
SELECT *
FROM Clientes c
INNER JOIN Cuentas cu
ON c.IdCliente = cu.IdCliente;
```

---

# Principio #9

## Limitar resultados

❌

```sql
SELECT *
FROM Transacciones;
```

---

✔

```sql
SELECT TOP 100 *
FROM Transacciones;
```

---

Beneficio:

```text
Menos datos transferidos.
```

---

# Principio #10

## Evitar subconsultas innecesarias

❌

```sql
SELECT *
FROM
(
    SELECT *
    FROM Clientes
) AS c;
```

---

✔

```sql
SELECT *
FROM Clientes;
```

---

# Caso bancario

## Problema

Buscar una cuenta.

### Consulta lenta

```sql
SELECT *
FROM Cuentas
WHERE NumeroCuenta = '123456';
```

---

### Optimización

```sql
CREATE INDEX IX_NumeroCuenta
ON Cuentas(NumeroCuenta);
```

---

Resultado:

```text
Miles de veces más rápida.
```

---

# Lecturas lógicas

SQL Server mide:

```text
Logical Reads
```

Cuántas páginas debe leer.

---

Consulta mala:

```text
100000 lecturas
```

---

Consulta optimizada:

```text
10 lecturas
```

---

# Costos principales

Una consulta consume:

```text
CPU
I/O
Memoria
Red
```

La optimización busca reducir estos costos.

---

# Error común

❌

```sql
SELECT *
```

en producción.

---

✔

```sql
SELECT columnas específicas
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
Si funciona, está optimizada.
```

Incorrecto.

Una consulta puede:

```text
Ser correcta
Pero extremadamente lenta.
```

---

# Pensamiento de DBA

Antes de ejecutar una consulta pregúntate:

1. ¿Existe un índice?
2. ¿Necesito todas las columnas?
3. ¿Necesito todas las filas?
4. ¿Estoy forzando un Table Scan?
5. ¿Cuántos registros procesará SQL?

---

# Checklist de optimización

Antes de publicar una consulta:

```text
□ Evité SELECT *
□ Utilicé WHERE
□ Revisé índices
□ Evité funciones innecesarias
□ Revisé JOINs
□ Limité resultados
□ Analicé el plan de ejecución
```

---

# Relación con otros conceptos

```text
INDEXES            → Aceleran consultas
QUERY OPTIMIZATION → Reduce costos
EXECUTION PLAN     → Explica cómo SQL ejecuta consultas
```

---

# Resumen

La optimización de consultas consiste en obtener los mismos resultados utilizando menos recursos.

Principios fundamentales:

- Evitar SELECT *
- Utilizar índices
- Filtrar temprano
- Evitar Table Scans
- Utilizar JOINs correctamente
- Analizar Execution Plans

Es una de las habilidades más importantes para:

- DBA
- SQL Developer
- Data Engineer
- Backend Engineer
- Database Engineer
