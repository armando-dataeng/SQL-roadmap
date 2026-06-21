# DYNAMIC SQL

## Definición

Dynamic SQL (SQL Dinámico) consiste en construir y ejecutar consultas SQL durante el tiempo de ejecución.

A diferencia del SQL tradicional:

```sql
SELECT *
FROM Clientes;
```

donde la consulta está definida desde el inicio,

en Dynamic SQL la consulta se construye mediante variables.

---

## Conceptos clave

Dynamic SQL responde a la pregunta:

> ¿Cómo puedo construir consultas dinámicamente según las necesidades del usuario o del sistema?

Características:

- Genera consultas dinámicamente.
- Permite flexibilidad.
- Se utiliza frecuentemente en Stored Procedures.
- Puede ejecutar SQL variable.
- Debe utilizarse cuidadosamente por motivos de seguridad.

---

# SQL Estático

## Ejemplo

```sql
SELECT *
FROM Clientes;
```

La consulta siempre será la misma.

---

# SQL Dinámico

## Ejemplo

```sql
DECLARE @SQL NVARCHAR(MAX);

SET @SQL =
'SELECT *
 FROM Clientes';

EXEC(@SQL);
```

---

## ¿Qué ocurre?

SQL almacena el texto:

```sql
SELECT *
FROM Clientes
```

dentro de una variable.

Posteriormente:

```sql
EXEC(@SQL);
```

ejecuta el contenido.

---

# Primer ejemplo

## Problema

Consultar una tabla cuyo nombre cambia.

### SQL

```sql
DECLARE @Tabla NVARCHAR(100);
DECLARE @SQL NVARCHAR(MAX);

SET @Tabla = 'Clientes';

SET @SQL =
'SELECT *
 FROM ' + @Tabla;

EXEC(@SQL);
```

---

## Resultado

```sql
SELECT *
FROM Clientes;
```

---

# Dynamic SQL con filtros

## Problema

Buscar clientes por ciudad.

### SQL

```sql
DECLARE @Ciudad NVARCHAR(50);
DECLARE @SQL NVARCHAR(MAX);

SET @Ciudad = 'Madrid';

SET @SQL =
'SELECT *
 FROM Clientes
 WHERE Ciudad = ''' + @Ciudad + '''';

EXEC(@SQL);
```

---

## Consulta generada

```sql
SELECT *
FROM Clientes
WHERE Ciudad = 'Madrid';
```

---

# Dynamic SQL dentro de Stored Procedures

## SQL

```sql
CREATE PROCEDURE sp_ConsultarTabla
(
    @Tabla NVARCHAR(100)
)
AS
BEGIN

    DECLARE @SQL NVARCHAR(MAX);

    SET @SQL =
    'SELECT *
     FROM ' + @Tabla;

    EXEC(@SQL);

END;
```

---

## Ejecución

```sql
EXEC sp_ConsultarTabla 'Clientes';
```

---

# Problema de seguridad

## SQL Injection

Dynamic SQL mal implementado puede permitir ataques.

Ejemplo peligroso:

```sql
DECLARE @Nombre NVARCHAR(100);

SET @Nombre =
''' OR 1=1 --';
```

Consulta generada:

```sql
SELECT *
FROM Clientes
WHERE Nombre = ''
OR 1=1;
```

Resultado:

```text
Devuelve todos los registros.
```

---

# Solución profesional

Utilizar:

```sql
sp_executesql
```

---

# sp_executesql

## Definición

Permite ejecutar SQL dinámico parametrizado.

Más seguro y eficiente.

---

## Ejemplo

```sql
DECLARE @SQL NVARCHAR(MAX);

SET @SQL =
'
SELECT *
FROM Clientes
WHERE IdCliente = @IdCliente
';

EXEC sp_executesql
    @SQL,
    N'@IdCliente INT',
    @IdCliente = 1;
```

---

## Ventajas

### Seguridad

Reduce riesgo de SQL Injection.

---

### Rendimiento

Permite reutilizar planes de ejecución.

---

### Legibilidad

Consultas más mantenibles.

---

# Caso bancario

## Problema

Consultar distintas tablas históricas.

### SQL

```sql
DECLARE @Anio VARCHAR(4);
DECLARE @SQL NVARCHAR(MAX);

SET @Anio = '2025';

SET @SQL =
'
SELECT *
FROM Transacciones_' + @Anio;

EXEC(@SQL);
```

---

## Consulta generada

```sql
SELECT *
FROM Transacciones_2025;
```

---

# Casos de uso reales

## Reporting

Seleccionar tablas según período.

```sql
Ventas_2024
Ventas_2025
```

---

## ETL

Procesar múltiples tablas automáticamente.

---

## Administración

Consultar bases de datos dinámicamente.

---

## Data Warehousing

Procesar particiones por fecha.

---

## Auditoría

Generar consultas automáticas.

---

# EXEC vs sp_executesql

## EXEC

```sql
EXEC(@SQL);
```

Más simple.

---

## sp_executesql

```sql
EXEC sp_executesql ...
```

Más seguro.

Más eficiente.

Recomendado para producción.

---

# Error común

❌ Incorrecto

```sql
SET @SQL =
'SELECT * FROM Clientes
 WHERE Nombre = ' + @Nombre;
```

---

✔ Correcto

```sql
EXEC sp_executesql
    @SQL,
    N'@Nombre NVARCHAR(100)',
    @Nombre = @Nombre;
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
Dynamic SQL siempre es mejor.
```

Incorrecto.

SQL estático suele ser:

```text
Más seguro.
Más simple.
Más rápido de mantener.
```

Dynamic SQL debe utilizarse únicamente cuando realmente se necesita flexibilidad.

---

# Pensamiento de DBA

Antes de utilizar Dynamic SQL pregúntate:

1. ¿Puedo resolverlo con SQL estático?
2. ¿Existe riesgo de SQL Injection?
3. ¿Necesito tablas dinámicas?
4. ¿Necesito columnas dinámicas?
5. ¿Debo usar sp_executesql?

---

# Relación con otros conceptos

```text
STORED PROCEDURE → Ejecuta lógica
FUNCTION         → Devuelve valores
TEMP TABLE       → Almacena resultados temporales
DYNAMIC SQL      → Genera consultas dinámicamente
```

---

# Resumen

Dynamic SQL permite construir consultas durante la ejecución.

Herramientas principales:

```sql
EXEC()
sp_executesql
```

Usos frecuentes:

- ETL
- Administración
- Reporting
- Data Warehousing
- Automatización

Buenas prácticas:

- Preferir SQL estático cuando sea posible.
- Utilizar sp_executesql.
- Evitar SQL Injection.
- Parametrizar consultas.

Es una herramienta avanzada que debe utilizarse con criterio y seguridad.
