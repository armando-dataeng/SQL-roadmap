# STORED PROCEDURES

## Definición

Un Stored Procedure (Procedimiento Almacenado) es un conjunto de instrucciones SQL almacenadas dentro de la base de datos.

Permite encapsular lógica de negocio y reutilizarla múltiples veces.

Se ejecuta bajo demanda mediante:

```sql
EXEC
```

o

```sql
EXECUTE
```

---

## Conceptos clave

Un Stored Procedure responde a la pregunta:

> ¿Cómo puedo reutilizar lógica SQL sin reescribirla constantemente?

Características:

- Reutilizable.
- Centraliza lógica de negocio.
- Mejora la seguridad.
- Facilita el mantenimiento.
- Puede recibir parámetros.
- Puede devolver resultados.

---

## Sintaxis básica

```sql
CREATE PROCEDURE NombreProcedimiento
AS
BEGIN

    SELECT *
    FROM Tabla;

END;
```

---

## Primer ejemplo

### Problema

Mostrar todos los clientes.

### SQL

```sql
CREATE PROCEDURE sp_ObtenerClientes
AS
BEGIN

    SELECT *
    FROM Clientes;

END;
```

---

## Ejecutar procedimiento

```sql
EXEC sp_ObtenerClientes;
```

---

## Resultado

```text
Todos los registros de Clientes.
```

---

# Procedimientos con parámetros

## Problema

Buscar un cliente específico.

### SQL

```sql
CREATE PROCEDURE sp_ObtenerCliente
    @IdCliente INT
AS
BEGIN

    SELECT *
    FROM Clientes
    WHERE IdCliente = @IdCliente;

END;
```

---

## Ejecución

```sql
EXEC sp_ObtenerCliente 1;
```

---

## Resultado

```text
Cliente con IdCliente = 1
```

---

# Múltiples parámetros

## Problema

Buscar cuentas con saldo mínimo.

### SQL

```sql
CREATE PROCEDURE sp_CuentasPorSaldo
    @SaldoMinimo DECIMAL(10,2)
AS
BEGIN

    SELECT *
    FROM Cuentas
    WHERE Saldo >= @SaldoMinimo;

END;
```

---

## Ejecución

```sql
EXEC sp_CuentasPorSaldo 10000;
```

---

# Procedimientos con CASE

## Problema

Clasificar clientes.

### SQL

```sql
CREATE PROCEDURE sp_ClasificarClientes
AS
BEGIN

    SELECT
        Nombre,
        Saldo,
        CASE
            WHEN Saldo >= 10000
                THEN 'VIP'
            ELSE 'Regular'
        END AS Categoria
    FROM Clientes;

END;
```

---

## Ejecución

```sql
EXEC sp_ClasificarClientes;
```

---

# Procedimientos con JOIN

## Problema

Mostrar clientes y cuentas.

### SQL

```sql
CREATE PROCEDURE sp_ClientesCuentas
AS
BEGIN

    SELECT
        c.Nombre,
        cu.NumeroCuenta,
        cu.Saldo
    FROM Clientes c
    INNER JOIN Cuentas cu
        ON c.IdCliente = cu.IdCliente;

END;
```

---

# Procedimientos con CTE

## SQL

```sql
CREATE PROCEDURE sp_ClientesVIP
AS
BEGIN

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

END;
```

---

# Procedimientos con Window Functions

## SQL

```sql
CREATE PROCEDURE sp_RankingClientes
AS
BEGIN

    SELECT
        Nombre,
        Saldo,
        RANK() OVER(
            ORDER BY Saldo DESC
        ) AS Ranking
    FROM Clientes;

END;
```

---

# Modificar procedimiento

```sql
ALTER PROCEDURE sp_ObtenerClientes
AS
BEGIN

    SELECT
        IdCliente,
        Nombre
    FROM Clientes;

END;
```

---

# Eliminar procedimiento

```sql
DROP PROCEDURE sp_ObtenerClientes;
```

---

# Casos de uso reales

## Sistema bancario

Transferencias.

```sql
EXEC sp_TransferirFondos;
```

---

## ETL

Carga de datos.

```sql
EXEC sp_CargarTransacciones;
```

---

## Reporting

Generación de reportes.

```sql
EXEC sp_GenerarReporteMensual;
```

---

## Business Intelligence

Actualización de métricas.

```sql
EXEC sp_ActualizarKPI;
```

---

# Ventajas

## Reutilización

Una sola implementación.

Múltiples ejecuciones.

---

## Seguridad

Permisos sobre el procedimiento.

No necesariamente sobre las tablas.

---

## Mantenimiento

La lógica se actualiza en un solo lugar.

---

## Rendimiento

SQL Server puede reutilizar planes de ejecución.

---

# Error común

❌ Incorrecto

```sql
CREATE PROCEDURE sp_Clientes

SELECT *
FROM Clientes;
```

✔ Correcto

```sql
CREATE PROCEDURE sp_Clientes
AS
BEGIN

    SELECT *
    FROM Clientes;

END;
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
Stored Procedure = Tabla
```

Incorrecto.

Un Stored Procedure es:

```text
Código SQL ejecutable.
```

No almacena datos.

---

# Convención de nombres

Muy utilizada en SQL Server:

```sql
sp_ObtenerClientes
sp_ClientesVIP
sp_GenerarReporte
sp_ActualizarSaldo
```

Prefijo:

```text
sp_
```

significa:

```text
Stored Procedure
```

---

# Pensamiento de Ingeniería de Datos

Antes de crear un procedimiento pregúntate:

1. ¿La lógica será reutilizada?
2. ¿Necesito parámetros?
3. ¿Necesito seguridad adicional?
4. ¿La lógica pertenece a la base de datos?
5. ¿Será ejecutado por aplicaciones o ETLs?

---

# Relación con otros conceptos

```text
VIEW                → Consulta reutilizable
CTE                 → Consulta temporal
FUNCTION            → Devuelve un valor
STORED PROCEDURE    → Ejecuta lógica SQL completa
```

---

# Resumen

Los Stored Procedures permiten encapsular lógica SQL reutilizable dentro de la base de datos.

Características:

- Reutilizables.
- Parametrizables.
- Seguros.
- Mantenibles.
- Escalables.

Son ampliamente utilizados en:

- SQL Server
- Sistemas bancarios
- ERP
- CRM
- ETL
- Data Engineering
- Business Intelligence
