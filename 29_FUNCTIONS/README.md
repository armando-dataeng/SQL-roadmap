# FUNCTIONS

## Definición

Una Function (Función) es un objeto de base de datos que recibe parámetros, ejecuta lógica y devuelve un resultado.

Las funciones permiten encapsular lógica reutilizable dentro de SQL Server.

Son similares a las funciones en lenguajes de programación como:

- Python
- Java
- C#
- JavaScript

---

## Conceptos clave

Una función responde a la pregunta:

> ¿Cómo puedo reutilizar una operación que devuelve un resultado?

Características:

- Recibe parámetros.
- Devuelve un valor o tabla.
- Puede reutilizarse en múltiples consultas.
- No modifica datos directamente.
- Puede utilizarse dentro de SELECT.

---

# Sintaxis básica

```sql
CREATE FUNCTION NombreFuncion
(
    @Parametro TipoDato
)
RETURNS TipoDato
AS
BEGIN

    RETURN Valor;

END;
```

---

# Primer ejemplo

## Problema

Calcular IVA.

### SQL

```sql
CREATE FUNCTION fn_CalcularIVA
(
    @Monto DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)
AS
BEGIN

    RETURN @Monto * 0.15;

END;
```

---

## Ejecutar función

```sql
SELECT dbo.fn_CalcularIVA(1000);
```

---

## Resultado

```text
150
```

---

# Función con múltiples parámetros

## Problema

Calcular interés.

### SQL

```sql
CREATE FUNCTION fn_CalcularInteres
(
    @Capital DECIMAL(10,2),
    @Tasa DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)
AS
BEGIN

    RETURN @Capital * @Tasa;

END;
```

---

## Ejecución

```sql
SELECT dbo.fn_CalcularInteres(10000,0.05);
```

---

## Resultado

```text
500
```

---

# Uso dentro de SELECT

## Problema

Calcular IVA para todas las cuentas.

### SQL

```sql
SELECT
    NumeroCuenta,
    Saldo,
    dbo.fn_CalcularIVA(Saldo) AS IVA
FROM Cuentas;
```

---

## Resultado esperado

| Cuenta | Saldo | IVA |
|---------|---------|---------|
| 1001 | 1000 | 150 |
| 1002 | 2000 | 300 |

---

# Funciones de tabla (Table-Valued Functions)

## Definición

Devuelven una tabla.

---

## SQL

```sql
CREATE FUNCTION fn_ClientesVIP()
RETURNS TABLE
AS
RETURN
(
    SELECT *
    FROM Clientes
    WHERE Saldo > 10000
);
```

---

## Ejecución

```sql
SELECT *
FROM dbo.fn_ClientesVIP();
```

---

## Resultado

```text
Clientes VIP
```

---

# Caso bancario

## Problema

Clasificar clientes.

### SQL

```sql
CREATE FUNCTION fn_CategoriaCliente
(
    @Saldo DECIMAL(10,2)
)
RETURNS VARCHAR(20)
AS
BEGIN

    RETURN
    (
        CASE
            WHEN @Saldo >= 50000 THEN 'Premium'
            WHEN @Saldo >= 10000 THEN 'VIP'
            ELSE 'Regular'
        END
    );

END;
```

---

## Uso

```sql
SELECT
    Nombre,
    Saldo,
    dbo.fn_CategoriaCliente(Saldo)
FROM Clientes;
```

---

# Casos de uso reales

## Finanzas

```sql
SELECT dbo.fn_CalcularInteres(5000,0.08);
```

---

## ETL

```sql
SELECT dbo.fn_NormalizarTelefono(Telefono);
```

---

## Business Intelligence

```sql
SELECT dbo.fn_CategoriaCliente(Saldo);
```

---

## Reporting

```sql
SELECT dbo.fn_FormatearNombre(Nombre);
```

---

# Diferencia entre Function y Stored Procedure

## Function

```sql
SELECT dbo.fn_CalcularIVA(1000);
```

Devuelve:

```text
Un valor.
```

---

## Stored Procedure

```sql
EXEC sp_ClientesVIP;
```

Ejecuta:

```text
Lógica SQL completa.
```

---

## Comparación

| Característica | Function | Procedure |
|----------------|-----------|------------|
| Devuelve valor | Sí | Opcional |
| Parámetros | Sí | Sí |
| Puede usarse en SELECT | Sí | No |
| Ejecuta procesos completos | No | Sí |
| Ideal para cálculos | Sí | No |

---

# Modificar función

```sql
ALTER FUNCTION fn_CalcularIVA
(
    @Monto DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)
AS
BEGIN

    RETURN @Monto * 0.18;

END;
```

---

# Eliminar función

```sql
DROP FUNCTION fn_CalcularIVA;
```

---

# Error común

❌ Incorrecto

```sql
CREATE FUNCTION fn_IVA
AS
BEGIN

    SELECT 100;

END;
```

---

✔ Correcto

```sql
CREATE FUNCTION fn_IVA()
RETURNS INT
AS
BEGIN

    RETURN 100;

END;
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
Function = Stored Procedure
```

Incorrecto.

Una Function:

```text
Devuelve un valor.
```

Un Procedure:

```text
Ejecuta lógica.
```

---

# Pensamiento de Ingeniería de Datos

Antes de crear una función pregúntate:

1. ¿Necesito devolver un valor?
2. ¿Necesito reutilizar cálculos?
3. ¿Debo utilizarla dentro de SELECT?
4. ¿La lógica es pequeña y específica?
5. ¿Un Stored Procedure sería excesivo?

---

# Relación con otros conceptos

```text
VIEW               → Consulta reutilizable
CTE                → Consulta temporal
FUNCTION           → Devuelve valor
STORED PROCEDURE   → Ejecuta lógica completa
```

---

# Resumen

Las Functions permiten encapsular lógica reutilizable dentro de SQL.

Ventajas:

- Reutilización.
- Modularidad.
- Mantenimiento.
- Legibilidad.

Son ampliamente utilizadas en:

- SQL Server
- Finanzas
- ETL
- Data Engineering
- Reporting
- Business Intelligence
