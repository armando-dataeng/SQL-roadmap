# EXECUTION PLANS

## Definición

Un Execution Plan (Plan de Ejecución) es la estrategia que utiliza SQL Server para ejecutar una consulta.

Antes de ejecutar una consulta, SQL Server analiza múltiples alternativas y selecciona la que considera más eficiente.

El Execution Plan muestra:

- Qué operaciones realizará SQL Server.
- Qué índices utilizará.
- Cuántas filas espera procesar.
- Qué operación consume más recursos.

---

## Conceptos clave

Un Execution Plan responde a la pregunta:

> ¿Cómo decidió SQL Server ejecutar mi consulta?

Permite comprender:

- Rendimiento.
- Cuellos de botella.
- Uso de índices.
- Costos de ejecución.

---

# ¿Por qué existen?

Consulta:

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 100;
```

SQL Server debe decidir:

```text
¿Leer toda la tabla?

o

¿Usar un índice?
```

La respuesta aparece en el Execution Plan.

---

# Tipos de Execution Plans

## Estimated Execution Plan

Plan estimado.

No ejecuta la consulta.

Muestra:

```text
Lo que SQL Server cree que ocurrirá.
```

---

## Actual Execution Plan

Plan real.

Ejecuta la consulta.

Muestra:

```text
Lo que realmente ocurrió.
```

---

# Obtener un Execution Plan

## SQL Server Management Studio

Atajo:

```text
Ctrl + M
```

Luego ejecutar la consulta.

---

## Menú

```text
Query
→ Include Actual Execution Plan
```

---

# Ejemplo simple

Consulta:

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 1;
```

Si existe índice:

```sql
CREATE INDEX IX_Clientes_Id
ON Clientes(IdCliente);
```

Plan:

```text
Index Seek
```

---

# Index Seek

## Definición

SQL utiliza un índice para localizar filas específicas.

Es una de las operaciones más eficientes.

---

## Ejemplo

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 1;
```

Plan:

```text
Index Seek
```

---

## Beneficio

```text
Pocas lecturas.
Menor tiempo.
```

---

# Table Scan

## Definición

SQL lee toda la tabla.

---

## Ejemplo

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Pedro';
```

Si no existe índice:

```text
Table Scan
```

---

## Problema

```text
Muchas lecturas.
Mayor tiempo.
```

---

# Clustered Index Scan

## Definición

SQL recorre el índice clustered completo.

---

## Ejemplo

```sql
SELECT *
FROM Clientes;
```

---

## ¿Siempre es malo?

No.

Si necesitas todas las filas:

```text
Es normal.
```

---

# Key Lookup

## Definición

Ocurre cuando SQL encuentra una fila mediante un índice pero necesita consultar columnas adicionales.

---

## Ejemplo

```sql
SELECT
    Nombre,
    Apellido,
    Direccion
FROM Clientes
WHERE Nombre = 'Pedro';
```

---

## Posible plan

```text
Index Seek
+
Key Lookup
```

---

## Problema

Miles de Key Lookups pueden ser costosos.

---

# Nested Loops

## Definición

Método utilizado para JOINs.

---

## Ejemplo

```sql
SELECT *
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Cuándo funciona bien

```text
Tablas pequeñas.
```

---

# Hash Match

## Definición

Método de JOIN utilizado en conjuntos grandes.

---

## Beneficio

```text
Escala mejor.
```

---

## Desventaja

```text
Consume más memoria.
```

---

# Sort

## Definición

Ordena resultados.

---

## Ejemplo

```sql
SELECT *
FROM Clientes
ORDER BY Nombre;
```

---

## Problema

Puede consumir:

```text
CPU
Memoria
```

---

# Cost Percentage

Cada operador tiene un costo estimado.

Ejemplo:

```text
Table Scan      80%
Sort            15%
Select           5%
```

---

## Interpretación

Normalmente se analiza:

```text
El operador más costoso.
```

---

# Caso bancario

Consulta:

```sql
SELECT *
FROM Cuentas
WHERE NumeroCuenta = '123456';
```

---

## Sin índice

Plan:

```text
Table Scan
```

Costo:

```text
Alto.
```

---

## Con índice

```sql
CREATE INDEX IX_NumeroCuenta
ON Cuentas(NumeroCuenta);
```

Plan:

```text
Index Seek
```

Costo:

```text
Bajo.
```

---

# Actual Rows vs Estimated Rows

Execution Plan muestra:

## Estimated Rows

```text
Filas estimadas.
```

---

## Actual Rows

```text
Filas reales.
```

---

## Problema

Si existe mucha diferencia:

```text
Las estadísticas pueden estar desactualizadas.
```

---

# Estadísticas

SQL Server utiliza estadísticas para estimar datos.

Actualizar:

```sql
UPDATE STATISTICS Clientes;
```

---

# Error común

Muchos desarrolladores observan:

```text
Tiempo de ejecución.
```

pero ignoran:

```text
Execution Plan.
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
La consulta más corta es la más rápida.
```

Incorrecto.

Lo importante es:

```text
El plan de ejecución.
```

---

# Pensamiento de DBA

Al revisar un Execution Plan pregúntate:

1. ¿Existe Table Scan?
2. ¿Existe Index Seek?
3. ¿Hay Key Lookups?
4. ¿Qué operador consume más costo?
5. ¿Las filas estimadas son correctas?

---

# Operadores importantes

```text
Index Seek
Index Scan
Table Scan
Clustered Index Scan
Key Lookup
Nested Loops
Hash Match
Sort
```

---

# Relación con otros conceptos

```text
INDEXES             → Aceleran consultas
QUERY OPTIMIZATION  → Mejora consultas
EXECUTION PLAN      → Explica cómo SQL ejecuta consultas
```

---

# Resumen

Los Execution Plans permiten visualizar cómo SQL Server ejecuta una consulta.

Ayudan a identificar:

- Scans innecesarios.
- Índices faltantes.
- Operadores costosos.
- Problemas de rendimiento.

Son una de las herramientas más importantes para:

- DBA
- SQL Developer
- Data Engineer
- Database Engineer
- Performance Tuning
