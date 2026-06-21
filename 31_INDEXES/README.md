# INDEXES

## Definición

Un Index (Índice) es una estructura de datos utilizada por el motor de base de datos para localizar registros más rápidamente.

Su propósito es reducir el tiempo necesario para encontrar información.

Puede compararse con el índice de un libro.

Sin índice:

```text
Debes leer todas las páginas.
```

Con índice:

```text
Vas directamente a la página correcta.
```

---

## Conceptos clave

Un índice responde a la pregunta:

> ¿Cómo puede SQL encontrar datos más rápido?

Características:

- Mejora consultas SELECT.
- Reduce lecturas innecesarias.
- Aumenta velocidad de búsqueda.
- Consume espacio adicional.
- Puede afectar INSERT, UPDATE y DELETE.

---

# ¿Por qué existen los índices?

Supongamos:

Tabla:

```text
Clientes
```

Registros:

```text
10 filas
```

SQL puede leer todo rápidamente.

---

Pero si la tabla tiene:

```text
10 millones de filas
```

Consulta:

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 5000000;
```

Sin índice:

```text
Table Scan
```

SQL revisa fila por fila.

---

Con índice:

```text
Index Seek
```

SQL encuentra el dato rápidamente.

---

# Crear un índice

## Sintaxis

```sql
CREATE INDEX NombreIndice
ON Tabla(Columna);
```

---

## Ejemplo

```sql
CREATE INDEX IX_Clientes_Nombre
ON Clientes(Nombre);
```

---

## ¿Qué mejora?

Consulta:

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Pedro';
```

Ahora SQL puede localizar registros más rápido.

---

# Clustered Index

## Definición

Determina el orden físico de almacenamiento de los datos.

Una tabla solo puede tener:

```text
1 Clustered Index
```

---

## Ejemplo

```sql
CREATE CLUSTERED INDEX IX_Clientes_Id
ON Clientes(IdCliente);
```

---

## ¿Por qué solo uno?

Porque una tabla solo puede almacenarse físicamente en un orden.

---

# Nonclustered Index

## Definición

Crea una estructura separada que apunta a los datos.

Una tabla puede tener:

```text
Muchos Nonclustered Indexes
```

---

## Ejemplo

```sql
CREATE NONCLUSTERED INDEX IX_Clientes_Apellido
ON Clientes(Apellido);
```

---

# Diferencia visual

## Clustered

```text
Datos ordenados físicamente.
```

---

## Nonclustered

```text
Índice separado.
Puntero hacia los datos.
```

---

# Caso bancario

## Problema

Buscar cuentas por número.

### SQL

```sql
SELECT *
FROM Cuentas
WHERE NumeroCuenta = '123456';
```

---

## Solución

```sql
CREATE INDEX IX_Cuentas_NumeroCuenta
ON Cuentas(NumeroCuenta);
```

---

## Beneficio

```text
Búsquedas mucho más rápidas.
```

---

# Índices compuestos

## Definición

Incluyen múltiples columnas.

---

## SQL

```sql
CREATE INDEX IX_Clientes_NombreApellido
ON Clientes
(
    Nombre,
    Apellido
);
```

---

## Consulta beneficiada

```sql
SELECT *
FROM Clientes
WHERE Nombre = 'Pedro'
AND Apellido = 'Lopez';
```

---

# Índices únicos

## Definición

Impiden valores duplicados.

---

## SQL

```sql
CREATE UNIQUE INDEX IX_Email
ON Clientes(Email);
```

---

## Resultado

```text
No permite correos duplicados.
```

---

# Ver índices existentes

### SQL Server

```sql
EXEC sp_helpindex 'Clientes';
```

---

# Eliminar índice

```sql
DROP INDEX IX_Clientes_Nombre
ON Clientes;
```

---

# Índices y JOINs

Consulta:

```sql
SELECT
    c.Nombre,
    cu.NumeroCuenta
FROM Clientes c
INNER JOIN Cuentas cu
    ON c.IdCliente = cu.IdCliente;
```

---

## Mejora recomendada

```sql
CREATE INDEX IX_Cuentas_IdCliente
ON Cuentas(IdCliente);
```

---

## Beneficio

JOIN más rápido.

---

# Table Scan vs Index Seek

## Table Scan

```text
Lee toda la tabla.
```

Costo:

```text
Alto.
```

---

## Index Seek

```text
Utiliza índice.
```

Costo:

```text
Bajo.
```

---

# Casos de uso reales

## Sistemas bancarios

```sql
NumeroCuenta
IdCliente
```

---

## E-commerce

```sql
ProductoID
CategoriaID
```

---

## Data Warehouse

```sql
Fecha
IdProducto
IdCliente
```

---

## ERP

```sql
NumeroFactura
```

---

# Error común

❌ Crear índices en todas las columnas.

```text
Mala práctica.
```

---

¿Por qué?

Cada:

```text
INSERT
UPDATE
DELETE
```

debe actualizar los índices.

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
Más índices = Más rendimiento.
```

Incorrecto.

Demasiados índices pueden:

- Consumir memoria.
- Aumentar almacenamiento.
- Ralentizar escrituras.

---

# ¿Qué columnas indexar?

Normalmente:

```text
PRIMARY KEY
FOREIGN KEY
WHERE
JOIN
ORDER BY
GROUP BY
```

---

## Ejemplo

```sql
WHERE IdCliente = ?
```

Buen candidato.

---

## Ejemplo

```sql
JOIN Clientes
ON IdCliente
```

Buen candidato.

---

# Pensamiento de DBA

Antes de crear un índice pregúntate:

1. ¿Esta columna se consulta frecuentemente?
2. ¿Participa en JOIN?
3. ¿Participa en WHERE?
4. ¿Participa en ORDER BY?
5. ¿El beneficio supera el costo?

---

# Relación con otros conceptos

```text
SELECT      → Consulta datos
JOIN        → Relaciona datos
INDEX       → Acelera consultas
```

---

# Resumen

Los índices permiten acelerar la búsqueda de datos.

Tipos principales:

```text
Clustered Index
Nonclustered Index
Unique Index
Composite Index
```

Son fundamentales para:

- SQL Server
- PostgreSQL
- Oracle
- MySQL
- DBA
- Database Engineering
- Data Engineering
- Optimización de consultas

Comprender índices es uno de los pilares del rendimiento en bases de datos.
